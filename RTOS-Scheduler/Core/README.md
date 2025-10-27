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

*   `SCHEDULER.c`: The core implementation of the RTOS scheduler, including the scheduling algorithm (e.g., round-robin, priority-based), context switching mechanisms, and managing task states (running, ready, blocked).
*   `button.c`: Implements the logic for reading and processing button inputs, often including debouncing algorithms to prevent false triggers.
*   `global.c`: Definitions and initializations of global variables and potentially common utility functions.
*   `main.c`: The application's entry point. It handles system initialization, peripheral configuration, creating initial tasks, and starting the RTOS kernel.
*   `stm32f1xx_hal_msp.c`: Implements the HAL MSP (MCU Specific Package) initialization functions. This file handles low-level hardware initialization for peripherals used by the HAL drivers, such as GPIOs, clocks, and DMA.
*   `stm32f1xx_it.c`: Contains the actual implementations of the interrupt service routines (ISRs) for the STM32F1xx microcontroller, handling events from peripherals and system exceptions.
*   `syscalls.c`: Provides the implementation for system calls, which are functions that allow user-level tasks to request services from the RTOS kernel in a controlled manner.
*   `sysmem.c`: Manages the system's memory, typically including the heap for dynamic memory allocation, and potentially providing functions for memory allocation and deallocation.
*   `system_stm32f1xx.c`: Contains functions responsible for configuring the system clock, Flash memory, and other fundamental microcontroller settings for the STM32F1xx series.
*   `task.c`: Implements the various task management functions, such as creating new tasks, changing task priorities, and handling task states.
*   `timer.c`: Implements the software timer functionalities, including managing timer lists, handling timer expirations, and executing timer callbacks.

### `Startup/` (Startup Files)
This directory contains the assembly startup file for the microcontroller.

*   `startup_stm32f103c6ux.s`: This is the assembly startup file specifically for the STM32F103C6 microcontroller. It handles the very first steps of microcontroller initialization after reset, including setting up the stack pointer, initializing the vector table (which maps interrupt vectors to their handlers), and eventually jumping to the `main` function in `main.c` to start the C application code.
