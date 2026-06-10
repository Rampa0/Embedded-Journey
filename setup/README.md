# STM32 Project Setup (Nucleo-F446 + CLion)

This guide walks through setting up an STM32 development environment using
**STM32CubeMX**, the **ARM GNU Toolchain**, **OpenOCD**, and **CLion**.

## Prerequisites

| Tool | Purpose |
| ---- | ------- |
| [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) | Generate project skeleton & peripheral config |
| [ARM GNU Toolchain](https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads) | Compiler, linker, and GDB debugger |
| [OpenOCD](https://openocd.org/) | Flashing and on-chip debugging |
| [CLion](https://www.jetbrains.com/clion/) | IDE / build & debug front-end |
| [Zadig](https://zadig.akeo.ie/) | Install the ST-Link USB driver on Windows |

## 1. Generate the project (STM32CubeMX)

1. Select the board: **Nucleo-F446**.
2. **Project Manager → Project → Toolchain/IDE:** select **CMake**.
3. Click **Generate Code** to create the project.

## 2. Install packages

1. Install **OpenOCD** and the **ARM GNU Toolchain**.
2. Note the path to `openocd.exe` — you'll point CLion at it in the next step.

## 3. Configure CLion

### Open the project

Open the generated CubeMX project folder in CLion.

### Toolchain — `Settings → Build, Execution, Deployment → Toolchains`

| Setting | Value |
| ------- | ----- |
| C compiler | `Arm-GNU-Toolchains\bin\arm-none-eabi-gcc.exe` |
| C++ compiler | `Arm-GNU-Toolchains\bin\arm-none-eabi-g++.exe` |
| Debugger | `Arm-GNU-Toolchains\bin\arm-none-eabi-gdb.exe` |
| Toolset | Bundled MinGW |
| CMake | Bundled |

### Run/Debug configuration — `Run → Edit Configurations`

1. Add a new **OpenOCD Download & Run** configuration.
2. **Board config file:** `board/st_nucleo_f4.cfg`
   *(CLion must be linked to `openocd.exe` for this to resolve.)*
3. **Executable binary:** `<file_name>.elf`

## 4. Install the Windows USB driver (Zadig)

1. Install and launch **Zadig**.
2. Plug the **Nucleo-F446** board into the PC.
3. Select the ST-Link device and install its driver.

## 5. Build & flash

Build the project and flash it onto the board using the Run/Debug
configuration created above.

---

> **Tip:** On the Nucleo-F446, `USART2` (PA2/PA3) is bridged to the onboard
> ST-Link Virtual COM Port, so `printf` output appears on the ST-Link serial
> port at **115200** baud, 8-N-1.
