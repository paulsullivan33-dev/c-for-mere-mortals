# Installing a Compiler

Unlike Python, C isn't run directly — it's **compiled**: translated to
machine code first, then executed. So you install a *compiler*, not an
interpreter. Pick your system below.

## Windows

The standard path is MSYS2, which provides GCC (the GNU compiler):

1. Download from [msys2.org](https://www.msys2.org/) and install.
2. Open the "MSYS2 UCRT64" terminal from the Start menu and run:

```bash
pacman -S --needed mingw-w64-ucrt-x86_64-gcc
```

3. Close that terminal. Open a **new PowerShell** and run:

```powershell
gcc --version
```

**Check:** a version number prints. If not, the installer's `bin`
folder isn't on your PATH — the MSYS2 installer offers to set this;
re-run it if needed. (Quicker alternative: [w64devkit](https://github.com/skeeto/w64devkit)
is a single zip you extract anywhere — no installer at all.)

## Mac

Apple ships the compiler with its developer tools. In Terminal:

```bash
xcode-select --install
```

Then:

```bash
cc --version
```

**Check:** a version number prints. (Mac's `cc` is Clang, which
compiles C just fine — the commands in these guides work the same.)

## Linux

Install GCC with your package manager. On Debian/Ubuntu:

```bash
sudo apt update && sudo apt install build-essential
```

Then:

```bash
gcc --version
```

**Check:** a version number prints.

## The compiler flags you'll use everywhere

Two flags appear in every guide here — learn them now:

- **`-Wall`** — turn on all the common warnings. The compiler *notices*
  many mistakes; this makes it tell you. Always use it.
- **`-g`** — include debugging info, so crashes can point at the
  guilty line. Always use it while learning.

You'll compile like this:

```bash
gcc -Wall -g program.c -o program
```

Next: [Your First Program](first-program.md).
