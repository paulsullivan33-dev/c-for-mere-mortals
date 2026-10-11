# Pointers

The concept C is famous for. A **pointer** is a variable that holds a
**memory address** — the location of another variable — instead of a
regular value. That's the whole idea. Everything else is notation.

## The two operators

```c
#include <stdio.h>

int main(void) {
    int x = 42;
    int *p = &x;          // p holds the ADDRESS of x

    printf("%d\n", *p);   // 42 — *p means "the value AT the address"
    *p = 100;             // change the value AT the address
    printf("%d\n", x);    // 100 — x itself changed
    return 0;
}
```

- `&x` — "address of x." Gives you a pointer.
- `*p` — "value at p." Follows the pointer to the variable.
- `int *p` — "p is a pointer to an int." The `*` in a declaration
  means something different from the `*` in an expression — same
  symbol, two jobs. (Everyone finds this confusing at first.)

## Why pointers exist

**1. Functions can't modify their arguments** (they get copies — see
[Functions](functions.md)). Pass the address instead:

```c
void double_it(int *x) {
    *x = *x * 2;   // modifies the caller's variable
}

int main(void) {
    int n = 5;
    double_it(&n);
    printf("%d\n", n);   // 10
    return 0;
}
```

**2. Arrays are pointers in disguise.** An array's name is the address
of its first element:

```c
int nums[3] = {10, 20, 30};
printf("%d\n", *nums);       // 10 — same as nums[0]
printf("%d\n", *(nums + 1)); // 20 — same as nums[1]
```

Pointer arithmetic moves by *elements*, not bytes: `nums + 1` is the
next `int`, wherever that lives.

**3. Dynamic memory** needs pointers to hold it — see
[Memory Basics](memory-basics.md).

## The rules that prevent disasters

- **Initialize every pointer.** `int *p;` points at garbage. Point it
  at something (`&x`) or at nothing (`NULL`) — never leave it
  dangling.
- **Never dereference `NULL`.** `*p` where `p` is `NULL` crashes
  immediately (segfault). Check before you dereference when a pointer
  might be empty.
- **A pointer doesn't own what it points to** unless you arranged that
  (with `malloc`). Don't `free()` something you didn't allocate.

Pointers feel alien for about a week, then click permanently. Draw
boxes and arrows on paper while learning — it genuinely helps.

Next: [Memory Basics](memory-basics.md).

## Sources

- [Beej's Guide: pointers](https://beej.us/guide/bgc/html/split/pointers.html)
