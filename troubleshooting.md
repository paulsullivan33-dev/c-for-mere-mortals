# Troubleshooting

C errors come in three flavors: the compiler refusing (good), the
linker refusing (annoying), and the program crashing (educational).
Each has its own habits.

## Read compiler errors top-down

Unlike Python (read tracebacks bottom-up), C's **first** error is
usually the real one — later errors often cascade from it. Fix the
first, recompile, repeat.

**Missing semicolon.** The classic. The error points at the *next*
line, not the guilty one — look upward:

```
error: expected ';' before '}' token
```

**Undeclared variable.** Typo or used before declaration. C reads top
to bottom; declare before use.

**Implicit declaration of function.** You called a function with no
visible declaration — usually a missing `#include` or a missing
prototype (see [Functions](functions.md)).

**Format specifier mismatch** (`-Wformat`, on with `-Wall`):
`printf("%d", 1.5)` — the `%d`/`%f` must match the argument. The
compiler warns; the running program prints garbage.

## Linker errors: "undefined reference"

```
undefined reference to `sqrt'
```

You *declared* it (via `#include <math.h>`) but never *linked* the
code. Math functions need `-lm`:

```bash
gcc -Wall -g program.c -o program -lm
```

Same error for your own functions means you forgot to list the `.c`
file on the compile line.

## Segfaults: the program crashed

"Segmentation fault" means the program touched memory it shouldn't —
usually a `NULL` dereference, an out-of-bounds array, or use-after-free
(see [Pointers](pointers.md), [Memory Basics](memory-basics.md)).

1. Recompile with `-g` (you already do, right?).
2. Run under a sanitizer or debugger:
   ```bash
   gcc -Wall -g -fsanitize=address program.c -o program
   ./program   # now the crash names the guilty line
   ```
3. Suspect the last pointer you touched.

## Debugging habits

- **`-Wall -Wextra`, always.** Treat warnings as errors while
  learning (`-Werror` makes the compiler enforce it).
- **Print the value.** `printf("x=%d\n", x)` before the crash line.
  Same as Python — it still works.
- **Shrink the program.** Delete half; if it still crashes, the bug
  is in the remaining half. Repeat.
- **Check the return values.** `malloc`, `fopen`, `scanf` all signal
  failure — ignoring them is how small bugs become segfaults.

## When to ask for help

Post: the full first error message (not the cascade), the smallest
complete program that reproduces it, the compile command, and what you
expected. "Undefined reference to sqrt, 20-line program, compiled
with gcc -Wall -g, expected it to link" gets answers.

Related: [Your First Program](first-program.md),
[Glossary](glossary.md).
