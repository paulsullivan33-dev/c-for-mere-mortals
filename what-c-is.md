# What C Is

C is a programming language from 1972 — old by software standards, and
still everywhere. Your operating system's kernel, the Python
interpreter itself, and the firmware in your microwave are largely C.
When people say "close to the metal," they usually mean C.

## What makes C different

Most modern languages hold your hand: they check your work, manage
memory for you, and stop you from touching things you shouldn't. C
does almost none of that. It gives you direct access to memory and
trusts you completely.

That trust is the whole deal:

- **You manage memory.** No garbage collector cleans up after you.
  You ask for memory, you give it back. Forget, and it leaks; give
  back twice, and things break. See [Memory Basics](memory-basics.md).
- **Types are strict and small.** An `int` is a fixed-size box of a
  fixed number of bytes. Put too big a number in and it wraps around
  silently — no warning.
- **Errors are terse.** The compiler tells you what's wrong in the
  fewest possible words, and segfaults tell you nothing at all. See
  [Troubleshooting](troubleshooting.md).

## Why learn it anyway

- **Understanding.** After C, you know what "a variable" actually is
  (a labeled spot in memory) and what every other language is doing
  for you behind the scenes.
- **Small machines.** Microcontrollers — Arduino, ESP32, and friends —
  run C and C++. If you want your code on real hardware, C is the
  language.
- **Speed and control.** Operating systems, game engines, and
  performance-critical libraries are C (or its descendant C++) because
  nothing gets between you and the machine.
- **It's the foundation.** C++, Java, C#, JavaScript, and Python's
  syntax all inherited from C. Learn C and every other language looks
  familiar.

## What it isn't

- **Not a beginner's first language anymore.** Python teaches
  programming ideas with far less friction. C teaches what the machine
  does — a different, harder lesson. Either order works; know which
  lesson you're signing up for.
- **Not memory-safe.** Whole categories of bugs (buffer overflows,
  use-after-free) that modern languages prevent are your personal
  responsibility in C.
- **Not dead.** People have predicted C's demise for decades. It's
  still in the top handful of languages by every measure, because the
  things it's good at haven't gone away.

Next: [Installing a Compiler](installing-a-compiler.md).

## Sources

- [C language reference (cppreference)](https://en.cppreference.com/w/c)
- [Beej's Guide to C Programming](https://beej.us/guide/bgc/)
