# Your First Program

C's workflow has one more step than Python's: **edit → compile → run**.
You write the code, the compiler translates it to a program, then you
run the program. Every C session follows this loop.

## 1. Write it

Create a file called `hello.c`:

```c
#include <stdio.h>

int main(void) {
    printf("Hello, world!\n");
    return 0;
}
```

Reading it line by line:

- `#include <stdio.h>` — borrow the standard input/output toolbox
  (that's where `printf` lives).
- `int main(void)` — every C program starts in a function called
  `main`. It returns an `int`: 0 means "all good."
- `printf(...)` — print formatted text. `\n` is a newline.
- Every statement ends with a **semicolon**. Forget one and the
  compiler complains.

## 2. Compile it

```bash
gcc -Wall -g hello.c -o hello
```

- `gcc` — the compiler.
- `-Wall -g` — warnings on, debugging info in. Always.
- `-o hello` — name the finished program `hello` (or `hello.exe`
  happens automatically on Windows).

**Check:** no output means success — silence is the compiler's praise.
A new file named `hello` (or `hello.exe`) should exist.

## 3. Run it

```bash
./hello        # Mac/Linux
.\hello.exe    # Windows PowerShell
```

**Check:** it prints `Hello, world!`.

## 4. Break it on purpose

Delete the semicolon after the `printf` line and compile again.

**Check:** the compiler errors — and points at the *next* line, not
the guilty one. This is normal: C reports where it *noticed* the
problem, which is often one line late. See
[Troubleshooting](troubleshooting.md). Put the semicolon back.

## What to try next

- [Variables and Types](variables-and-types.md): storing data.
- [Control Flow](control-flow.md): decisions and loops.
- [Functions](functions.md): reusable chunks.

## Sources

- [Beej's Guide: Hello World](https://beej.us/guide/bgc/html/split/hello-world.html)
