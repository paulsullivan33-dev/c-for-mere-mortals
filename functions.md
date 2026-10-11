# Functions

Same idea as Python — named, reusable chunks — with two C-specific
twists: you declare the function's *shape* before use, and every
function states what it returns.

## Defining and calling

```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main(void) {
    int result = add(2, 3);
    printf("%d\n", result);   // 5
    return 0;
}
```

- `int add(int a, int b)` — takes two `int`s, returns an `int`.
- A function returning nothing is declared `void`:

```c
void greet(void) {
    printf("Hello!\n");
}
```

## Declaration vs. definition

C reads top to bottom: it must *know about* a function before you call
it. If the definition comes after `main`, add a **declaration**
(prototype) up top:

```c
#include <stdio.h>

int add(int a, int b);   // declaration: "trust me, it exists"

int main(void) {
    printf("%d\n", add(2, 3));
    return 0;
}

int add(int a, int b) {  // definition: the actual code
    return a + b;
}
```

Call a function with no visible declaration and the compiler errors
("implicit declaration"). With `-Wall`, it errors loudly — good.

## Headers: shared declarations

Real programs split across files. Declarations live in **header files**
(`.h`), shared with `#include`:

```c
/* mathutils.h */
int add(int a, int b);
```

```c
/* mathutils.c */
int add(int a, int b) {
    return a + b;
}
```

```c
/* main.c */
#include <stdio.h>
#include "mathutils.h"   // quotes = "my project", brackets = system

int main(void) {
    printf("%d\n", add(2, 3));
    return 0;
}
```

Compile all the `.c` files together:

```bash
gcc -Wall -g main.c mathutils.c -o program
```

## Arguments are copies

C passes arguments **by value** — the function gets a copy. Changing
the parameter inside doesn't touch the caller's variable:

```c
void double_it(int x) {
    x = x * 2;   // only the copy changes
}

int main(void) {
    int n = 5;
    double_it(n);
    printf("%d\n", n);   // still 5
    return 0;
}
```

To let a function modify the caller's variable, pass its address —
which is what [Pointers](pointers.md) are for.

Next: [Pointers](pointers.md).

## Sources

- [Beej's Guide: functions](https://beej.us/guide/bgc/html/split/functions.html)
