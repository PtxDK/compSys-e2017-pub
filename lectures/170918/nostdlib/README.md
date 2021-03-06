# `.c` → `.o` → `.bin`

This directory showcases the workflow in the main stages of a compiler and/or
how to build and run minimal C programs.

`make src/42.c` will use GCC to compile the C file into a binary file
`src/42.bin`, _without_ relying on a standard library.

(We use the unconventional extension `.bin` for executable to make them easier
to deal with en masse.)

The peace of magic that makes this possible is the [`_start.s`](_start.s) file.
This file is prepended to each assembly file before it is built. This file
calls the `main` label in your assembly file, and expects you to have written
the exit code to `%eax` upon return.

We call [`_start.s`](_start.s) "magic" because it makes a _system call_: it
calls on the system to exit with the given exit code. System calls will be
covered in much more detail later on in the course.

There are some other specialized, phony targets in the [`Makefile`](Makefile)
which you might find useful:

* `make dump-42.bin` uses `objdump` to dump the assembly of `src/42.bin`.
* `make gdb-42.bin` fires up a GDB session with `src/42.bin`, assuming that
  there also exists a GDB script `src/42.gdb`.
