

Dynamic memory is where C gives you **maximum power and zero safety nets**. Mastering it means you can build flexible programs; misunderstanding it leads to crashes, leaks, and undefined behavior.

This file explains **how the heap works**, **how ownership works**, and **how to avoid classic memory bugs**.

---

## 1. Stack vs Heap (Quick Recap)

|Stack|Heap|
|---|---|
|Automatic lifetime|Manual lifetime|
|Very fast|Slightly slower|
|Fixed size|Large & flexible|
|Freed on return|Freed by programmer|

Use the heap when:

- Size is not known at compile time
    
- Data must outlive a function call
    

---

## 2. malloc – Allocate Memory

```c
int *arr = malloc(10 * sizeof(int));
```

What happens:

- Heap memory is reserved
    
- Contents are **uninitialized**
    
- Pointer returned to first byte
    

⚠️ Always check the result:

```c
if (!arr) {
    // allocation failed
}
```

---

## 3. calloc – Allocate and Zero

```c
int *arr = calloc(10, sizeof(int));
```

Differences from `malloc`:

- Memory is initialized to zero
    
- Slightly slower
    
- Safer defaults
    

---

## 4. free – Release Memory

```c
free(arr);
arr = NULL;
```

Rules:

- Only free what you allocated
    
- Free exactly once
    
- Never use memory after free
    

Setting to `NULL` prevents accidental reuse.

---

## 5. Ownership (Critical Concept)

> The function that allocates memory **owns** it and is responsible for freeing it — unless ownership is explicitly transferred.

Example:

```c
int *makeArray(int n) {
    return malloc(n * sizeof(int));
}
```

Caller owns the memory and must `free` it.

---

## 6. Common Allocation Patterns

### Dynamic arrays

```c
int *arr = malloc(n * sizeof *arr);
```

### Struct allocation

```c
Person *p = malloc(sizeof *p);
```

This style avoids type mismatches.

---

## 7. Reallocation with realloc

```c
arr = realloc(arr, newSize);
```

- May move memory
    
- Old pointer becomes invalid
    
- If realloc fails, original pointer is unchanged
    

Safe pattern:

```c
int *tmp = realloc(arr, newSize);
if (tmp) arr = tmp;
```

---

## 8. Memory Leaks

Occurs when:

- Memory is allocated but never freed
    
- Pointer to allocated memory is lost
    

Example:

```c
void leak() {
    int *x = malloc(sizeof *x);
}
```

Leak detection tools:

- Valgrind
    
- AddressSanitizer
    

---

## 9. Use-After-Free Bugs

```c
free(arr);
arr[0] = 10; // ❌ UB
```

One of the most dangerous bugs in C.

---

## 10. Double Free

```c
free(arr);
free(arr); // ❌ UB
```

Often causes crashes or heap corruption.

---

## 11. Dynamic 2D Arrays

### Pointer-to-pointer approach

```c
int **mat = malloc(rows * sizeof *mat);
for (int i = 0; i < rows; i++)
    mat[i] = malloc(cols * sizeof *mat[i]);
```

Must free in reverse order.

---

## 12. Memory and Your Repository

Dynamic memory appears in:

- File reading buffers
    
- Variable-size arrays
    
- Data structures
    

Correct `malloc/free` placement is repeatedly emphasized.

---

## 13. Best Practices

✅ Always check allocation results

✅ Free memory in the same logical layer

✅ Set freed pointers to NULL

✅ Prefer clear ownership rules

---

## 14. Key Takeaway

> Dynamic memory is powerful, but **discipline is mandatory**.

If you lose track of ownership, C will not save you.

---

_End of dynamic_memory.md_