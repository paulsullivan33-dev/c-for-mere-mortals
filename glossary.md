# Glossary

Quick definitions, A to Z. Terms point to the guide that explains
them in context.

**Address** — a variable's location in memory. `&x` gives it.

**Buffer overflow** — writing past the end of an array, corrupting
whatever sat next to it. A classic C bug.

**Compiler** — translates C source into machine code. GCC and Clang
are the common ones.

**Declaration** — announcing a function's shape (name, parameters,
return type) before use. See [Functions](functions.md).

**Dereference** — following a pointer to its value: `*p`.

**Double free** — freeing the same heap memory twice. Corrupts the
allocator.

**Garbage collector** — automatic memory cleanup, which C does *not*
have. You do it yourself.

**Header file** — shared declarations in a `.h` file, pulled in with
`#include`.

**Heap** — memory you request with `malloc` and return with `free`.
See [Memory Basics](memory-basics.md).

**Linker** — combines compiled pieces (and libraries) into the final
program. "Undefined reference" is its complaint.

**malloc / free** — request and return heap memory. Every malloc needs
a free.

**NULL** — a pointer to nothing. Dereferencing it crashes.

**Pointer** — a variable holding a memory address. See
[Pointers](pointers.md).

**Preprocessor** — the pass before compiling that handles `#include`
and `#define`.

**Prototype** — another word for a function declaration.

**Segfault** — crash from touching memory you shouldn't. Short for
segmentation fault.

**sizeof** — operator reporting a type's size in bytes. Never assume
sizes.

**Stack** — automatic memory for local variables. Dies with the
function.

**Static typing** — variable types are fixed when declared, unlike
Python.

**Undefined behavior** — the standard's way of saying "anything can
happen, including seeming to work." Avoid, don't exploit.

**Warning** — the compiler noticing something suspicious. With
`-Wall`, read every one.
