# Memory Basics

C gives you two places to put data: the **stack** (automatic, easy)
and the **heap** (manual, powerful). Most beginner programs live
entirely on the stack. The heap is where C's reputation comes from.

## The stack: variables as usual

```c
int main(void) {
    int x = 42;        // lives on the stack
    int nums[100];     // also the stack — fixed size, automatic cleanup
    return 0;          // everything above vanishes here, safely
}
```

Local variables and fixed-size arrays live on the stack. They're
created when the function starts and destroyed when it returns —
automatically, no action needed. **Limitation:** the size must be known
when you write the code, and the memory dies with the function. You
can't return a stack array to the caller (it stops existing).

## The heap: memory on demand

When the size isn't known until the program runs — user input, file
contents — ask for memory with `malloc`:

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
    int n = 5;
    int *nums = malloc(n * sizeof(int));  // room for n ints

    if (nums == NULL) {
        printf("out of memory\n");
        return 1;
    }

    nums[0] = 42;
    printf("%d\n", nums[0]);

    free(nums);   // give it back — required
    return 0;
}
```

- `malloc(size)` asks for bytes; `sizeof(int)` keeps it portable.
- **Always check for `NULL`** — malloc fails when memory runs out.
- **`free()` everything you `malloc`.** Every single time, on every
  path out of the function.

## The three heap sins

1. **Leak** — forgetting `free()`. The memory stays claimed until the
   program ends. In long-running programs, leaks accumulate and kill.
2. **Use after free** — touching memory you gave back. It might work,
   might crash, might corrupt something else. Never do it.
3. **Double free** — freeing the same pointer twice. Corrupts the
   allocator's bookkeeping; crashes in confusing places.

One owner per allocation: decide which part of the code is responsible
for freeing, and document it in a comment.

## Tools that catch what you miss

- **AddressSanitizer:** compile with `-fsanitize=address` — it finds
  leaks, overflows, and use-after-free at runtime with clear reports.
- **Valgrind:** runs your program under a microscope (`valgrind
  ./program`). Slower, thorough, no recompilation needed.

Use one of them while learning. They turn "mysterious crash" into "line
17, use after free" — the difference between an hour and a minute.

Next: [Troubleshooting](troubleshooting.md).

## Sources

- [Beej's Guide: dynamic memory](https://beej.us/guide/bgc/html/split/manual-memory-management.html)
