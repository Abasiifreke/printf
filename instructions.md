# 0x11. C - printf

- Project to be done in teams of 2 people (your team: Abas Ubon, Alexander Udeogaranya)
- Project was started on Mar 24, 2023 6:00 AM, and ended by Mar 29, 2023 before 6:00 AM

## Concepts

For this project, we expect you to look at these concepts:

- [Group Projects]()
- [Pair Programming - How To]()
- [Flowcharts]()
- [Technical Writing]()

## Background Context

Write your own printf function.

## Read or Watch:

- [Secrets of printf]()
- [Group Projects concept page (Don’t forget to read this)]()
- [Flowcharts concept page]()

## Man or Help:

- `printf (3)`

## Authorized Functions and Macros

- `write (man 2 write)`
- `malloc (man 3 malloc) `
- `free (man 3 free)`
- `va_start (man 3 va_start)`
- `va_end (man 3 va_end)`
- `va_copy (man 3 va_copy)`
- `va_arg (man 3 va_arg)`

## Compilation

The code will be compiled this way:

- `$ gcc -Wall -Werror -Wextra -pedantic -std=gnu89 *.c`

  ```bash
  alex@ubuntu:~/c/printf$ cat main.c
  #include <limits.h>
  #include <stdio.h>
  #include "main.h"

  /**
   * main - Entry point
   *
   * Return: Always 0
   */
  int main(void)
  {
      int len;
      int len2;
      unsigned int ui;
      void *addr;

      len = _printf("Let's try to printf a simple sentence.\n");
      len2 = printf("Let's try to printf a simple sentence.\n");
      ui = (unsigned int)INT_MAX + 1024;
      addr = (void *)0x7ffe637541f0;
      _printf("Length:[%d, %i]\n", len, len);
      printf("Length:[%d, %i]\n", len2, len2);
      _printf("Negative:[%d]\n", -762534);
      printf("Negative:[%d]\n", -762534);
      _printf("Unsigned:[%u]\n", ui);
      printf("Unsigned:[%u]\n", ui);
      _printf("Unsigned octal:[%o]\n", ui);
      printf("Unsigned octal:[%o]\n", ui);
      _printf("Unsigned hexadecimal:[%x, %X]\n", ui, ui);
      printf("Unsigned hexadecimal:[%x, %X]\n", ui, ui);
      _printf("Character:[%c]\n", 'H');
      printf("Character:[%c]\n", 'H');
      _printf("String:[%s]\n", "I am a string !");
      printf("String:[%s]\n", "I am a string !");
      _printf("Address:[%p]\n", addr);
      printf("Address:[%p]\n", addr);
      len = _printf("Percent:[%%]\n");
      len2 = printf("Percent:[%%]\n");
      _printf("Len:[%d]\n", len);
      printf("Len:[%d]\n", len2);
      _printf("Unknown:[%r]\n");
      printf("Unknown:[%r]\n");
      return (0);
  }
  alex@ubuntu:~/c/printf$ gcc -Wall -Wextra -Werror -pedantic -std=gnu89 -Wno-format *.c
  alex@ubuntu:~/c/printf$ ./printf
  Let's try to printf a simple sentence.
  Let's try to printf a simple sentence.
  Length:[39, 39]
  Length:[39, 39]
  Negative:[-762534]
  Negative:[-762534]
  Unsigned:[2147484671]
  Unsigned:[2147484671]
  Unsigned octal:[20000001777]
  Unsigned octal:[20000001777]
  Unsigned hexadecimal:[800003ff, 800003FF]
  Unsigned hexadecimal:[800003ff, 800003FF]
  Character:[H]
  Character:[H]
  String:[I am a string !]
  String:[I am a string !]
  Address:[0x7ffe637541f0]
  Address:[0x7ffe637541f0]
  Percent:[%]
  Percent:[%]
  Len:[12]
  Len:[12]
  Unknown:[%r]
  Unknown:[%r]
  alex@ubuntu:~/c/printf$
  ```

- Write a function that produces output according to a format.

  - Prototype: `int _printf(const char *format, ...);`
  - Returns: the number of characters printed (excluding the null byte used to end output to strings)
  - write output to `stdout`, the standard output stream
    format is a character string. The format string is composed of zero or more directives. See `man 3 printf` for more detail. You need to handle the following conversion specifiers:
    - `c`
    - `s`
    - `%`
  - You don’t have to reproduce the buffer handling of the C library printf function
  - You don’t have to handle the flag characters
  - You don’t have to handle field width
  - You don’t have to handle precision
  - You don’t have to handle the length modifiers

- Handle the following conversion specifiers:

  - `d`
  - `i`
  - You don’t have to handle the flag characters
  - You don’t have to handle field width
  - You don’t have to handle precision
  - You don’t have to handle the length modifiers

- Handle the following custom conversion specifiers:

  - `b`: the unsigned int argument is converted to binary

  ```bash
  alex@ubuntu:~/c/printf$ cat main.c
  #include "main.h"

  /**
   * main - Entry point
   *
   * Return: Always 0
   */
  int main(void)
  {
      _printf("%b\n", 98);
      return (0);
  }
  alex@ubuntu:~/c/printf$ gcc -Wall -Wextra -Werror -pedantic -std=gnu89 main.c
  alex@ubuntu:~/c/printf$ ./a.out
  1100010
  alex@ubuntu:~/c/printf$
  ```

- Handle the following conversion specifiers:

  - `u`
  - `o`
  - `x`
  - `X`
  - You don’t have to handle the flag characters
  - You don’t have to handle field width
  - You don’t have to handle precision
  - You don’t have to handle the length modifiers

- Use a local buffer of `1024` chars in order to call write as little as possible.

- Handle the following custom conversion specifier:

  - `S` : prints the string.
  - Non printable characters (0 < ASCII value < 32 or >= 127) are printed this way: \x, followed by the ASCII code value in hexadecimal (upper case - always 2 characters)

  ```bash
  alex@ubuntu:~/c/printf$ cat main.c
  #include "main.h"

  /**
   * main - Entry point
   *
   * Return: Always 0
   */
  int main(void)
  {
      _printf("%S\n", "Best\nSchool");
      return (0);
  }
  alex@ubuntu:~/c/printf$ gcc -Wall -Wextra -Werror -pedantic -std=gnu89 main.c
  alex@ubuntu:~/c/printf$ ./a.out
  Best\x0ASchool
  alex@ubuntu:~/c/printf$
  ```

- Handle the following conversion specifier: `p`.

  - You don’t have to handle the flag characters
  - You don’t have to handle field width
  - You don’t have to handle precision
  - You don’t have to handle the length modifiers

- Handle the following flag characters for non-custom conversion specifiers:

  - `+`
  - `space`
  - `#`

- Handle the following length modifiers for non-custom conversion specifiers:

  - `l`
  - `h`

- Conversion specifiers to handle: `d`, `i`, `u`, `o`, `x`, `X`

- Handle the field width for non-custom conversion specifiers.

- Handle the precision for non-custom conversion specifiers.

- Handle the 0 flag character for non-custom conversion specifiers.

- Handle the - flag character for non-custom conversion specifiers.

- Handle the following custom conversion specifier:

  - `r` : prints the reversed string

- Handle the following custom conversion specifier:

  - `R`: prints the rot13'ed string

- All the above options work well together.

