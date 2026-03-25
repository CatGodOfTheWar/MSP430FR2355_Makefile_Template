# MSP430FR2355 Bare-Metal Development Environment 

A clean, cross-platform bare-metal development environment for the **Texas Instruments MSP430FR2355** microcontroller. This repository provides isolated `Makefiles` for both Windows and Linux (Fedora/Ubuntu), handling compilation, flashing, static analysis, and code formatting without relying on heavy IDEs like Code Composer Studio.

## Features
* **Isolated Environments:** Clean separation between Windows and Linux build setups.
* **Bare-Metal:** Uses the official `msp430-elf-gcc` toolchain.
* **Native Flashing:** Integrates TI's `DSlite.exe` (via the included `.ccxml` target file) for Windows and `mspdebug` for Linux.
* **Quality Assurance:** Built-in targets for `cppcheck` (static analysis) and `clang-format` (styling).

## Project Structure

.
├── LICENSE                
├── README.md               
├── Linux_Makefile/         
│   └── Makefile           
└── Windows_Makefile/       
    ├── Makefile            
    └── MSP-EXP430FR2355LP.ccxml 

*(Note: Add your source `.c` and `.h` files to the root directory or a dedicated `src/` folder, and update the `SOURCES` variable in the respective `Makefile`)*

## Prerequisites

Ensure you have the following installed on your system before proceeding:

1. **[MSP430 GCC Open Source Compiler](https://www.ti.com/tool/MSP430-GCC-OPENSOURCE):** The core C/C++ compiler.
2. **[Code Composer Studio (CCS)](https://www.ti.com/tool/CCSTUDIO) or UniFlash:** Required *only* for the debug drivers (`DSlite.exe` or `mspdebug`).
3. **Make:** * **Linux:** Native `make` (e.g., `sudo dnf install make`).
   * **Windows:** Install [MSYS2](https://www.msys2.org/) or use **Git Bash** to have access to standard Unix commands like `make`, `rm`, and `mkdir`.
4. **Code Tools (Optional but recommended):** `cppcheck` and `clang-format`.

## How to Build and Flash

Navigate to the directory that matches your operating system, then run the standard `make` commands.

### On Linux (Fedora/Ubuntu)
cd Linux_Makefile 

make all

make flash 

### On Windows (via Git Bash / MSYS2)
cd Windows_Makefile

make all

make flash 

## Available Commands

Run these commands inside the `Windows_Makefile` or `Linux_Makefile` directory:

| Command | Description |
| :--- | :--- |
| `make all` | Compiles the source code and generates the final binary. |
| `make clean` | Removes the auto-generated `build/` directory and compiled objects. |
| `make flash` | Uploads the compiled firmware to the MSP430 board. |
| `make cppcheck` | Runs static analysis to find potential bugs or memory issues. |
| `make format` | Formats the C code according to standard styling rules. |
| `make size` | Displays the memory footprint (RAM/Flash usage) of the binary. |
| `make symbols` | Lists the compiled symbols sorted by memory address. |

## Adding Source Files

When you add new `.c` files to your project, you must update the `SOURCES` variable inside the respective `Makefile` (Windows or Linux):

# Inside Makefile
SOURCES = ../main.c ../led.c ../my_new_driver.c

*(Adjust the relative path `../` based on where you store your C files relative to the Makefile).*

## License
Distributed under the MIT License. See `LICENSE` for more information.
