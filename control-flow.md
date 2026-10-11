# Control Flow

Same three tools as every language — `if`, `for`, `while` — but with
braces `{}` marking blocks and semicolons ending statements. Python
uses indentation; C uses punctuation. Get the punctuation right and
the logic is familiar.

## if: making decisions

```c
#include <stdio.h>

int main(void) {
    int age = 20;

    if (age >= 18) {
        printf("adult\n");
    } else {
        printf("minor\n");
    }
    return 0;
}
```

Chain with `else if`:

```c
if (score >= 90) {
    printf("A\n");
} else if (score >= 80) {
    printf("B\n");
} else {
    printf("F\n");
}
```

**The `=` vs `==` trap:** `if (x = 5)` *assigns* 5 to x (always true);
`if (x == 5)` *compares*. The compiler warns about the first with
`-Wall` — read the warning.

## for: counting loops

```c
for (int i = 0; i < 5; i++) {
    printf("%d\n", i);   // 0 1 2 3 4
}
```

The three parts, in order: **start** (`int i = 0`), **keep going while**
(`i < 5`), **each round do** (`i++`, meaning add one). Miss the
semicolons between them and nothing compiles.

## while: repeating until something changes

```c
int count = 3;
while (count > 0) {
    printf("%d\n", count);
    count--;
}
printf("go!\n");
```

If the condition never becomes false, the loop never ends — Ctrl+C
stops a runaway program in the terminal, same as Python.

## switch: choosing among many values

```c
char grade = 'B';

switch (grade) {
    case 'A':
        printf("excellent\n");
        break;
    case 'B':
        printf("good\n");
        break;
    default:
        printf("keep practicing\n");
}
```

**Don't forget `break`.** Without it, execution *falls through* into
the next case — occasionally useful, usually a bug. The compiler
warns about it; listen.

Next: [Functions](functions.md).

## Sources

- [Beej's Guide: flow control](https://beej.us/guide/bgc/html/split/control-flow.html)
