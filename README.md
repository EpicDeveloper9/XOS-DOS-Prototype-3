XOS-DOS (P3) - Version 25.12.13
===============================

A simple 16-bit real-mode operating system written in x86 assembly (NASM).
Boots from a floppy image and provides a DOS-like command-line interface.

Features
--------
- Classic command prompt
- Startup splash screen
- Built-in commands: cls, ver, time, date, dir, help, print, exit, restart
- Text file system (.xtxt files)
  - Create and edit with `newtext filename.xtxt` (end with a single '.' on its own line)
  - View with `vwf filename.xtxt`
  - List with `dir`
- Simple scripting
  - Create scripts with `xprg` (end with 'end_prg.')
  - Run with `run`
  - Supports print, variables (%VAR%), set /VAR="value", and goto

Requirements
------------
- NASM assembler
- MSYS2 or Linux environment
- QEMU for testing

Build Instructions
------------------
1. Open MSYS2 terminal in the folder.
2. Run:
   	nasm -f bin boot.asm -o boot.bin
   	nasm -f bin kernel.asm -o kernel.bin
3. Create the floppy image (example using dd on Linux/MSYS2):
   	dd if=/dev/zero of=xos.img bs=512 count=2880
   	dd if=boot.bin of=xos.img conv=notrunc
   	dd if=kernel.bin of=xos.img bs=512 seek=1 conv=notrunc

Run
---
qemu-system-i386 -fda xos.img

Commands
--------
cls            - Clear screen
ver            - Show version
time           - Show current time
date           - Show current date
dir            - List files
help           - Show this command list
print <text>   - Print text
exit           - Halt the OS
restart        - Restart the OS
newtext file.xtxt - Create/edit text file
vwf file.xtxt  - View text file
xprg           - Create a script (CURRENTLY BEING TESTED SO IT DOESN'T WORK)
run            - Run the last script

Scripting (xprg)
---------------
- print <text>         : Print text
- print %VAR%          : Print variable value
- set /VAR="value"     : Set variable
- goto N               : Jump to line N
- Lines starting with : are labels

License
-------
MIT License

Copyright (c) 2025 EpicDeveloper

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

Enjoy XOS-DOS!
