# LC3 Virtual Machine for mcpp
[![made-with-cpp](https://img.shields.io/badge/Made%20with-C++_17-1f425f.svg)](https://cplusplus.com/) [![creator-justinmeiners](https://img.shields.io/badge/Creator-justinmeiners-008000.svg)](https://github.com/justinmeiners) [![adapted-by-rozukke](https://img.shields.io/badge/Adapted_by-rozukke-f497af.svg)](https://github.com/rozukke) [![GitHub license](https://img.shields.io/github/license/rozukke/lc3-vm-mcpp.svg)](https://github.com/rozukke/lc3-vm-mcpp/blob/main/LICENSE)

This is a C++ based virtual machine for the LC3 assembly language, adapted to work with [mcpp](https://github.com/rozukke/mcpp) the Royal Melbourne Institute of Technology (RMIT) to supplement the COSC2084 (Programming Studio 2) course. The original project by [Justin Meiners](https://github.com/justinmeiners) can be found [here](https://github.com/justinmeiners/lc3-vm). Thank you to [Michael Dann](https://github.com/mchldann/) for the original adaptation and trap implementations.

## Additions
This VM supports a few additional TRAPs based on mcpp functionality, including:
- `CHAT` to post to Minecraft chat
- `GETP` to get player position
- `SETP` to set player position
- `GETB` to get block type
- `SETB` to set block type
- `GETH` to get max height at an x,z coordinate
As well as:
- `REG` to print out registers to console. By default, it will print as `unsigned`, but the VM supports flags to print as:
    - `-d` signed
    - `-x` hexadecimal
    - `-b` binary

## Usage
`lc3 [-FLAG] <file.obj>` where `file.obj` is a [compiled](https://github.com/rozukke/laser-mcpp) binary. `-FLAG` is a single letter flag based on the above Additions section.

## Installation
Designed to install on UNIX-based systems. Run `make` in the root directory and then `sudo make install` to make the command globally available.

## TRAP formats

| TRAP | **mcpp** function    | Description |
| ---- | -------------------- | --------------------------------------- |
| CHAT | postToChat(R0)       | Outputs a null terminating string starting at the address contained in R0 to the Minecraft chat. |
| GETP | getPlayerPosition() -> R0, R1, R2 | Gets the position of the player. The x, y and z coordinates are output in registers R0, R1 and R2 respectively. |
| SETP | setPlayerPosition(R0, R1, R2) | This function moves the player to the tile (x, y, z) = (R0, R1, R2). |
| GETB | getBlock(R0, R1, R2) -> R3 | This function retrieves the block's ID at tile (x, y, z) = (R0, R1, R2) and returns it to R3. |
| SETB | setBlock(R0, R1, R2, R3) | This function changes the ID of the block at tile (x, y, z) = (R0, R1, R2) to the value stored in R3. |
| GETH | getHeight(R0, R2) -> R1 | This function calculates the y-position of the highest non-air block at (x, z) = (R0, R2) and returns the value to R1. |
| REG | **Non-mcpp** | Debugging function to print registers to console. See above for alternative print modes. |

## Examples
Two `.asm` examples are provided, printing a "Hello World" message in the console and in Minecraft. Run the `.obj` files to test the code out. 
