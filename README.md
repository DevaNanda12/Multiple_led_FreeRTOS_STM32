# FreeRTOS LED Blinking with STM32 Nucleo F446RE

## Overview

This project demonstrates the use of FreeRTOS with STM32 Nucleo-F446RE to create and manage multiple tasks that could control GPIO-connected LEDs. The application initializes the system, configures GPIOs, and creates three RTOS tasks. Although the LED toggling logic isn't implemented yet, the structure is ready for further development.

## Features

- Uses **FreeRTOS** for multitasking.
- Three threads created using `osThreadCreate()`:
  - `defaultTask`
  - `Led1Task`
  - `Led2Task`
- Each task currently runs an infinite loop with a delay (`osDelay(1)`), prepared for future logic like LED blinking.
- GPIO initialization for:
  - PA5 (commonly connected to on-board LED)
  - PB0 (user-configurable output)

## Hardware Requirements

- STM32 Nucleo-F446RE Development Board
- USB cable for power and programming
- Optional: External LEDs connected to PA5 and PB0

## Software Requirements

- STM32CubeIDE
- STM32CubeMX (optional for reconfiguration)
- HAL and CMSIS-RTOS (FreeRTOS) libraries

## Code Summary

### main.c

- **`main()`**:
  - Initializes HAL, system clock, and GPIO.
  - Creates three tasks using `osThreadDef` and `osThreadCreate`.
  - Starts the FreeRTOS scheduler.

- **`SystemClock_Config()`**:
  - Configures system clock using HSI (High Speed Internal oscillator) with PLL.

- **`MX_GPIO_Init()`**:
  - Enables GPIO clocks and configures PA5 and PB0 as output push-pull pins with no pull-up/down.

- **Tasks**:
  - `StartDefaultTask`, `StartTask02`, `StartTask03` — currently contain infinite loops with 1ms delay, ready for user-defined actions.

- **Error_Handler()**:
  - Disables interrupts and enters an infinite loop on critical failure.

### Threads

| Task Name     | Stack Size | Priority         | Function         | Purpose                        |
|---------------|------------|------------------|------------------|--------------------------------|
| defaultTask   | 128        | Normal (default) | `StartDefaultTask` | Idle or system monitoring     |
| Led1Task      | 128        | Normal           | `StartTask02`      | Intended for LED 1 control    |
| Led2Task      | 128        | Normal           | `StartTask03`      | Intended for LED 2 control    |

## Getting Started

1. Clone or download the project.
2. Open it in STM32CubeIDE.
3. Connect the STM32 Nucleo board via USB.
4. Build and flash the project to the board.
5. (Optional) Modify task bodies (`StartTask02`, `StartTask03`) to implement LED toggling or other logic.

## Potential Extensions

- Add toggling logic in `StartTask02` and `StartTask03` using `HAL_GPIO_TogglePin()`.
- Use semaphores or queues for task synchronization.
- Interface with UART or sensors to trigger LED behavior.

## License

This software is provided "AS IS" under STMicroelectronics' licensing terms. See the LICENSE file if available.
## Author

Deva Nanda S

