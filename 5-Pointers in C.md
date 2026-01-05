

Pointers are the **core abstraction of C**. If arrays and strings felt tricky, pointers are the reason. Mastering pointers means you understand **memory, performance, and control**.

This file aims to make pointers _mechanical_, not mystical.

---

## 1. What a Pointer Is

A pointer is a variable that **stores a memory address**.

```c
int x = 10;
int *p = &x;
```

- `x` stores a value
    
- `p` stores the address of `x`
    

---

## 2. Address-of and Dereferencing

```c
int x = 5;
int *p = &x;

printf("%d", *p); // 5
```

- `&x` → address of `x`
    
- `*p` → value at address stored in `p`
    

⚠️ `*` means **different things** depending on context.

---

## 3. Pointer Types Matter

```c
int *ip;
double *dp;
```

The type determines:

- How many bytes are read/written when dereferencing
    
- How pointer arithmetic behaves
    

All pointers are the same **size** (8 bytes on 64-bit), but not the same **type**.

---

## 4. Pointer Arithmetic

```c
int arr[5] = {1,2,3,4,5};
int *p = arr;

p + 1; // moves by sizeof(int)
```

Equivalent:

```c
arr[2] == *(arr + 2)
```

This explains how arrays and pointers are connected.

---

## 5. Pointers and Arrays

```c
int arr[3];
int *p = arr;
```

- `arr` → address of first element
    
- `&arr` → address of entire array
    

```c
sizeof(arr); // 12
sizeof(p);   // 8
```

Very common exam trap.

---

## 6. Null Pointers

```c
int *p = NULL;
```

- Represents "points to nothing"
    
- Dereferencing NULL → crash
    

Always initialize pointers.

---

## 7. Pointers as Function Parameters

Pointers enable **pass-by-reference**.

```c
void swap(int *a, int *b) {
  int tmp = *a;
  *a = *b;
  *b = tmp;
}
```

Used heavily in your repository.

---

## 8. Pointers to Pointers

```c
int x = 10;
int *p = &x;
int **pp = &p;
```

Used when:

- Modifying a pointer itself
    
- Dynamic 2D arrays
    
- Command-line arguments
    

---

## 9. const and Pointers

```c
const int *p;   // pointer to const int
int *const p;   // const pointer
const int *const p;
```

Know this distinction — it appears in exams.

---

## 10. Dangling Pointers

```c
int *p;
{
  int x = 5;
  p = &x;
}
*p; // ❌ UB
```

Occurs when pointing to:

- Freed memory
    
- Stack memory that went out of scope
    

---

## 11. Pointer Pitfalls

Common errors:

- Dereferencing uninitialized pointers
    
- Using freed memory
    
- Wrong pointer arithmetic
    
- Confusing `*` and `&`
    

---

## 12. Pointers in Your Repository

Seen in:

- Dynamic arrays
    
- Passing structs to functions
    
- File I/O buffers
    
- GUI state management
    

These examples show **real usage**, not toy examples.

---

## 13. Mental Model

> A pointer is just a number interpreted as an address.

The type tells C how to use it — not the hardware.

---

## 14. Best Practices

✅ Initialize pointers

✅ Use NULL checks

✅ Match pointer type with data

✅ Free what you allocate

---

_End of pointers.md_