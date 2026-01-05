
This file collects **the most common C exam traps** — the kind of code that _looks_ correct, compiles cleanly, and still fails. Each section explains **why it’s a trap**, what the examiner expects, and how to reason your way out.

Use this as a **pre-exam checklist**.

---

## 1. Returning Address of a Local Variable

```c
int *f() {
    int x = 10;
    return &x; // TRAP
}
```

Why it’s wrong:

- `x` lives on the stack
    
- Stack frame disappears on return
    
- Returned pointer dangles
    

Correct fixes:

- Allocate on heap
    
- Pass pointer into function
    

---

## 2. sizeof Pointer vs sizeof Object

```c
int *p = malloc(10 * sizeof(p)); // TRAP
```

Why it’s wrong:

- `sizeof(p)` is size of pointer, not int
    

Correct:

```c
malloc(10 * sizeof *p);
```

---

## 3. Off-by-One Errors

```c
for (int i = 0; i <= 10; i++) {
    arr[i] = 0; // TRAP
}
```

Arrays indexed `0..9`.

Correct condition:

```c
i < 10
```

---

## 4. Assignment vs Comparison

```c
if (x = 0) { } // TRAP
```

Why it’s tricky:

- Legal C syntax
    
- Always false
    

Defensive style:

```c
if (x == 0)
```

---

## 5. Using Uninitialized Variables

```c
int x;
if (x > 0) { } // TRAP
```

Local variables are **not initialized**.

Always initialize explicitly.

---

## 6. Modifying String Literals

```c
char *s = "abc";
s[0] = 'A'; // TRAP
```

String literals are read-only.

Correct:

```c
char s[] = "abc";
```

---

## 7. Missing NULL Check After malloc

```c
int *p = malloc(sizeof *p);
*p = 5; // TRAP
```

Examiner expects:

```c
if (!p) {
    // handle error
}
```

---

## 8. Using freed Memory

```c
free(p);
printf("%d", *p); // TRAP
```

Classic use-after-free.

Correct pattern:

```c
free(p);
p = NULL;
```

---

## 9. Forgetting break in switch

```c
switch (x) {
    case 1:
        f();
    case 2:
        g(); // TRAP
}
```

Fall-through unless `break`.

---

## 10. Assuming Array Size in Function

```c
void f(int arr[]) {
    int n = sizeof(arr) / sizeof(arr[0]); // TRAP
}
```

Arrays decay to pointers.

Correct:

- Pass size explicitly
    

---

## 11. Signed vs Unsigned Comparisons

```c
int i = -1;
unsigned u = 1;
if (i < u) { } // TRAP
```

Implicit conversion flips logic.

---

## 12. fgets vs scanf

```c
scanf("%s", buf); // TRAP
```

No bounds checking.

Prefer:

```c
fgets(buf, sizeof buf, stdin);
```

---

## 13. Multiple frees on same pointer

```c
free(p);
free(p); // TRAP
```

Heap corruption.

---

## 14. Confusing Pointer and Value Semantics

```c
void f(int x) {
    x = 5;
}
```

Does NOT modify caller.

Use pointer to modify.

---

## 15. The "Looks Right" Trap

Code that:

- Compiles
    
- Produces output
    
- Is still wrong
    

Exams love this.

Always simulate execution step-by-step.

---

## 16. How Examiners Think

They test:

- Memory lifetime
    
- Ownership
    
- Undefined behavior
    

Not syntax.

---

## 17. Final Exam Rule

> If something feels "too easy", it’s probably a trap.

Slow down. Analyze memory.

---

_End of exam_traps.md_