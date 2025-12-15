XOS-DOS Readme
Overview
XOS-DOS is a custom, lightweight, 16-bit operating system written in NASM assembly, designed to run on real hardware or emulators. It features a command-line shell with many classic DOS-inspired commands, a simple scripting language (via XPRG and RUN), a colorful startup screen, and a PC speaker startup tune.
Version: 25.12.15 (December 15, 2025)
It boots from a floppy disk image (xos.img) and provides a fun, retro DOS-like experience.
Features

Beautiful blue startup screen with logo and version
PC speaker startup melody (C-E-G-C)
Full command shell with > prompt
Case-insensitive commands
Built-in scripting (XPRG to create, RUN to execute)
Over 20 commands (see list below)

Available Commands













































































































CLS -Clears the screen

VER - Shows OS version

TIME - Shows current system time

DATE - Shows current system date

DIR / LS - Shows directory listing (simulated)

HELP - Shows basic command list

HELP /ADV - Shows detailed help for all commands

EXIT - Halts the system

RESTART - Restarts the OS (full startup sequence again)

BEEP - Plays the startup tune

PWD - Prints current directory (A:)

MEM - Shows conventional memory size

PRINT <text> - Prints the given text

ECHO <text> - Same as PRINT

TYPE <file> - Displays fake file content

MKDIR <dir> - Creates a fake directory

CD <dir> - Changes current fake directory

DEL <file> - Deletes a fake file

REN <old> <new> - Renames a fake file

FORMAT - Formats the fake disk

CHKDSK - Checks disk (simulated)

TREE - Shows directory tree

VOL - Shows volume label

XPRG - Create a simple script program

RUN - Run the last created program

Scripting (XPRG)

Type XPRG to enter program mode
Enter lines one by one
Type a single . on a line to finish and save
Supported script commands:
set /VAR="value" – sets a variable
print "text" or print %VAR% – prints text or variable
goto N – jumps to line N (0-based)
Labels with :label (ignored for now)


Example:
textXPRG
> set /W_MSG="Hello World!"
> print %W_MSG%
> .
RUN
Building and Running
Requirements

NASM assembler
QEMU or Bochs (for testing)
DOSBox (best for hearing the beep tune)
dd, mkfs.vfat (Linux/Mac)

Build Steps
Bash# Assemble
nasm -f bin boot.asm -o boot.bin
nasm -f bin kernel.asm -o kernel.bin

# Create 1.44MB floppy image
dd if=/dev/zero of=xos.img bs=1024 count=1440
mkfs.vfat -F 12 xos.img

# Mount and copy files
mkdir mnt
sudo mount -o loop xos.img mnt
sudo cp boot.bin mnt/BOOT.SYS
sudo cp kernel.bin mnt/KERNEL.SYS
sudo umount mnt
rmdir mnt

# Write bootloader to MBR
dd if=boot.bin of=xos.img bs=512 count=1 conv=notrunc
Run

QEMU (with sound for beep):Bashqemu-system-i386 -fda xos.img -soundhw pcspk
DOSBox (excellent sound):
Mount the directory and boot the image.
Bochs or real hardware via USB/floppy.

Troubleshooting

No startup screen or beep: Use DOSBox or QEMU with -soundhw pcspk.
"Bad command" on first prompt: Fixed in current version — empty lines are now ignored.
Scripts not running: Make sure to end with a single . on its own line.

Credits
Created with love by a retro computing enthusiast.
Inspired by classic MS-DOS and FreeDOS
