# Clipboard tools for DOS.

Goal for this project is start wide usage clipboard into DOS programs.
Win3 (and great) provide API for DOS, but clean DOS (and some emulators)
have no. So, I think, need create standalone driver and command-line tool.

## ClipDRV

Clipboard driver for DOS.

* Provide Win3-clipboard API (INT 2F, AX=1700..170A). See Q67675.TXT
* Provide clipboard up to 64k.
* Support copy text screen to cliboard via `PrintScreen` key. In case
when ClipDRV does not handle video mode (graphics or VESA) - pass call to
previous INT 5 handler.
* Support monochrome adapters (like Hercules) with $B000 video-memory segment.
* Require 128kb of XMS memory.

ClipDRV does not support VESA modes - only 1, 2, 3, 7, 8 video modes.

## ClipCLI

Command-line interface for clipboard.

ClipCLI allow one of two parameters: C or P (case-insens).

C mean copy, P - paste.

ClipCLI read STDIN and copy to clipboard for C,
and get data from clipboard and print to STDOUT for P.

If STDIN is not redirected, ClipCLI get text from keyboard.
In this case, you can use ^Z or ^D as end of input (eof).

Usage examples:

     clipcli.com C < myfile.txt

will copy file myfile.txt to clipboard

     clipcli.com P

will print clipboard to STDOUT.

Also, you can use `clipcli copy` or `clipcli paste` (only first
char is checked and must be 'c' or 'p', case-insens).

# API & Documentation

See Q67675.TXT

# Build

Go to directory SRC and type

        make

# License

MIT License. See LICENSE.TXT file.

This repository contains SPHINX C-- compiler by Peter Cellik
and Michael Shecker, which have GREENWARE License, see TOOLS\LICENSE.TXT

https://github.com/DosWorld/clipdrv/
