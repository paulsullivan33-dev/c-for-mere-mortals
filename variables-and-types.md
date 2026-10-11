# Variables and Types

A variable in C is a named, fixed-size box in memory. Unlike Python,
you must say **what kind** of box when you create it — and the box
never changes kind afterward.

## The types you'll use daily

```c
int age = 36;            // whole number (usually 4 bytes)
float height = 1.65f;    // decimal, single precision (the f matters)
double precise = 1.654321; // decimal, double precision — the default choice
char grade = 'A';        // ONE character — single quotes, not double
```

Notes a Python user will trip on:

- `"A"` (double quotes) is a *string*; `'A'` (single quotes) is a
  single character. Different things.
- `1.65` without the `f` is a `double`; assigning it to a `float`
  without `f` draws a compiler warning. Use `double` unless you have
  a reason not to.
- Exact sizes vary by platform (`int` is *at least* 2 bytes, usually
  4). `sizeof(int)` tells you on your machine — never assume.

## Printing: you must say the type

C's `printf` doesn't know what you gave it — you tell it with a
**format specifier**:

```c
int age = 36;
double height = 1.65;
char grade = 'A';

printf("age %d, height %f, grade %c\n", age, height, grade);
```

| Specifier | Type |
|---|---|
| `%d` | `int` |
| `%f` | `float` / `double` |
| `%c` | `char` |
| `%s` | string (a `char` array — see [Pointers](pointers.md)) |

**Mismatch is a classic bug:** `printf("%d", 1.65)` prints garbage —
the compiler warned you (`-Wall`), the program didn't care. Match
every specifier to its argument.

## Unsigned and bigger integers

```c
unsigned int count = 4000000000u;  // only 0 and up, roughly double the max
long big = 9000000000L;            // at least 8 bytes on most 64-bit systems
```

Plain `int` tops out around ±2.1 billion. Exceed it and the value
**wraps around silently** — no error, just wrong. If your numbers can
grow, size the box accordingly.

## Two habits that prevent bugs

- **Compile with `-Wall` and read every warning.** Most C bugs announce
  themselves at compile time if you let them.
- **Initialize every variable.** `int x;` holds whatever garbage was
  in that memory. `int x = 0;` holds zero. Always initialize.

Next: [Control Flow](control-flow.md).

## Sources

- [cppreference: fundamental types](https://en.cppreference.com/w/c/language/type)
