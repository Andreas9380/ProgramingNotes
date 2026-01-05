
C gives you **full control** over memory and execution — and with it, the ability to crash your program in spectacular ways. This file catalogs the **most common errors**, why they happen, how to recognize them, and how to prevent them.

These are the mistakes that appear in:

- Exams
    
- Assignments
    
- Real-world C code
    

---

## 1. Segmentation Faults (Segfaults)

A segmentation fault occurs when your program accesses memory it is **not allowed** to access.

### Common causes

- Dereferencing NULL pointers
    
- Accessing freed memory
    
- Out-of-bounds array access
    

Example:

```c
int *p = NULL;
*p = 10; // segfault
```

---

## 2. Undefined Behavior (UB)

Undefined Behavior means:

> The C standard gives **no guarantees** about what happens.

### Examples

```c
int x = 0;
int y = x / x; // UB (division by zero)
```

```c
int a[5];
a[10] = 3; // UB
```

UB may:

- Crash
    
- Appear to work
    
- Fail later
    

---

## 3. Uninitialized Variables

```c
int x;
printf("%d", x); // garbage value
```

Occurs frequently with:

- Local variables
    
- Dynamically allocated memory
    

Fix:

```c
int x = 0;
```

---

## 4. Buffer Overflows

```c
char buf[10];
strcpy(buf, "This string is too long"); // UB
```

Consequences:

- Memory corruption
    
- Security vulnerabilities
    

Prevention:

- Track buffer sizes
    
- Use bounded functions
    

---

## 5. Use-After-Free

```c
int *p = malloc(sizeof *p);
free(p);
*p = 5; // UB
```

Often hard to debug.

Fix:

```c
free(p);
p = NULL;
```

---

## 6. Double Free

```c
free(p);
free(p); // UB
```

Can corrupt the heap.

---

## 7. Memory Leaks

```c
void f() {
    malloc(100);
}
```

Symptoms:

- Increasing memory usage
    
- Program slowdown
    

Prevention:

- Clear ownership rules
    
- Valgrind
    

---

## 8. Dangling Pointers

```c
int *p;
{
    int x = 5;
    p = &x;
}
*p; // UB
```

Points to memory that no longer exists.

---

## 9. Mixing Signed and Unsigned

```c
int i = -1;
unsigned int u = 1;

if (i < u) {
    // false due to implicit conversion
}
```

Classic exam trap.

---

## 10. Wrong sizeof Usage

```c
int *p = malloc(10 * sizeof(p)); // WRONG
```

Correct:

```c
malloc(10 * sizeof *p);
```

---

## 11. Forgetting Function Prototypes

Calling functions before declaration leads to:

- Implicit int (older C)
    
- Wrong calling conventions
    

Always declare in headers.

---

## 12. Modifying String Literals

```c
char *s = "Hello";
s[0] = 'h'; // UB
```

Fix:

```c
char s[] = "Hello";
```

---

## 13. Incorrect Pointer Arithmetic

```c
int *p;
p += 4; // meaningless unless initialized
```

Pointer arithmetic depends on type and base address.

---

## 14. Tools to Catch Errors

- **Valgrind** – memory issues
    
- **AddressSanitizer** – runtime checks
    
- **Compiler warnings** (`-Wall -Wextra`)
    

Treat warnings as errors.

---

## 15. How These Errors Appear in Your Repo

Many exercises intentionally expose you to:

- Memory discipline
    
- Pointer safety
    
- Correct free placement
    

Learning to avoid these errors is the real goal.

---

## 16. Key Takeaway

> In C, _wrong code often compiles successfully_.

Correctness is the programmer’s responsibility.

---

_End of common_errors.md_