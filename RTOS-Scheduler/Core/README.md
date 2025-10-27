# Core Folder Logic

This `Core` folder contains the fundamental logical components and source code for the RTOS-Scheduler project.

## Overview
The files within this directory are responsible for:
- Initializing the microcontroller.
- Managing tasks and their execution.
- Handling system-level interrupts and exceptions.
- Implementing core RTOS functionalities such as context switching, scheduling algorithms, and inter-task communication mechanisms.

## Detailed Components

### `Inc/` (Header Files)
This directory contains header files (`.h`) which declare functions, data structures, and macros used throughout the project.

*   `SCHEDULER.h`: Declarations for the RTOS scheduler's public interface, including task control block (TCB) definitions, ready queue management, and functions for task scheduling and context switching.
*   `button.h`: Contains declarations for functions and data structures related to handling button inputs, such as debouncing and state detection.
*   `global.h`: Defines global variables, common macros, and shared data types used across different modules of the RTOS.
*   `main.h`: The primary header file for the application, typically including other necessary headers and defining general project configurations, peripheral handles, and application-specific function prototypes.
*   `stm32f1xx_hal_conf.h`: Configuration file for the STM32 HAL (Hardware Abstraction Layer) drivers, used to enable or disable specific peripherals and set their operational parameters.
*   `stm32f1xx_it.h`: Declarations for the interrupt service routines (ISRs) for various peripherals and system exceptions on the STM32F1xx microcontroller.
*   `task.h`: Contains declarations for task-related functions and data structures, such as task creation, deletion, suspension, resumption, and other task management operations.
*   `timer.h`: Declarations for functions and data structures related to software timer management within the RTOS, enabling time-based events and delays.

### `Src/` (Source Files)
This directory contains source files (`.c`) which implement the functionalities declared in the header files.

*   `SCHEDULER.c`: This file embodies the heart of the RTOS, implementing the chosen scheduling algorithm (e.g., Round-Robin, Preemptive Priority, Rate Monotonic). It manages the ready queue of tasks, handles context switching between tasks, and updates task states (running, ready, blocked, suspended). Key functions would include `SCHEDULER_Init()`, `SCHEDULER_Start()`, `SCHEDULER_AddTask()`, and the core context switch mechanism.
*   `button.c`: Implements the debouncing logic for physical button inputs. It typically includes functions to initialize button GPIOs, read button states, and filter out spurious presses/releases. It might also contain state machines to detect short presses, long presses, or double clicks, and trigger corresponding events or callbacks.
*   `global.c`: This file usually contains the definitions and initializations of global variables, constants, and possibly simple utility functions that are shared across multiple source files but don't belong to a specific module. It helps in centralizing common resources and configurations.
*   `main.c`: The entry point of the entire application (`main()` function). It is responsible for the initial setup of the microcontroller (clock, peripherals, etc.), initializes the RTOS kernel, creates the initial set of tasks, and then starts the RTOS scheduler. After the scheduler starts, control is handed over to the RTOS, and the `main()` function typically does not return.
*   `stm32f1xx_hal_msp.c`: This file contains the implementation of the STM32 HAL (Hardware Abstraction Layer) MSP (MCU Specific Package) callbacks. These callbacks are invoked by the HAL drivers to perform low-level hardware initializations (e.g., GPIO clock enabling, configuring NVIC for interrupts, DMA setup) that are specific to the particular microcontroller and application board. It bridges the generic HAL drivers with the specific hardware configuration.
*   `stm32f1xx_it.c`: This file contains the Interrupt Service Routines (ISRs) for various peripherals and system exceptions (e.g., SysTick, EXTI, Timers, USART) of the STM32F1xx microcontroller. When an interrupt occurs, the corresponding function in this file is executed. These ISRs often call HAL interrupt handlers or custom application-specific interrupt handling logic.
*   `syscalls.c`: Implements the system calls (or system service calls) that allow user-level tasks to interact with the RTOS kernel in a protected and controlled manner. This typically involves using a software interrupt or a dedicated instruction to switch from unprivileged to privileged mode, allowing tasks to request services like memory allocation, task creation, or semaphore operations from the kernel.
*   `sysmem.c`: This file is dedicated to memory management within the system. It typically implements or configures the heap for dynamic memory allocation (e.g., `malloc`, `free` equivalents for embedded systems). In an RTOS context, it might also manage memory pools or provide mechanisms for safe memory allocation and deallocation across different tasks.
*   `system_stm32f1xx.c`: This file contains functions responsible for setting up the fundamental system aspects of the STM32F1xx microcontroller. This includes configuring the system clock tree (HSI, HSE, PLL settings), Flash memory latency, and other essential low-level configurations required before the main application code or RTOS can execute reliably.
*   `task.c`: Implements the core functionalities for managing individual tasks within the RTOS. This includes functions for creating and deleting tasks, changing their priorities, suspending and resuming tasks, and managing task-specific data. It often interacts closely with the scheduler to update task states and queues.
*   `timer.c`: Implements the software timer management. This includes functions to create, start, stop, and reset software timers. These timers are typically managed by a dedicated RTOS task or an interrupt service routine that periodically checks for timer expirations and executes associated callback functions.

### `Startup/` (Startup Files)
This directory contains the assembly startup file for the microcontroller.

*   `startup_stm32f103c6ux.s`: This is the assembly startup file specifically for the STM32F103C6 microcontroller. It handles the very first steps of microcontroller initialization after reset, including setting up the stack pointer, initializing the vector table (which maps interrupt vectors to their handlers), and eventually jumping to the `main` function in `main.c` to start the C application code.
