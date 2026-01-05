
Arrays are **contiguous memory blocks** used to store multiple values of the same type. Understanding arrays is crucial because they underpin **strings, matrices, and most data structures**.

---

## 1. Declaring Arrays

### Syntax

```c
int arr[10];  // 10 elements of type int
```

- Elements are indexed `0` to `9`
    
- Memory is contiguous
    
- Size must be known at compile-time for static arrays
    

### Initialization

```c
int arr[5] = {1, 2, 3, 4, 5};
int arr2[] = {1, 2, 3};  // Compiler deduces size
```

---

## 2. Accessing Elements

```c
arr[0] = 10;
int x = arr[4];
```

- Array name decays into pointer in expressions
    
- Bounds are **not checked** by C
    
- Out-of-bounds access = Undefined Behavior
    

---

## 3. Arrays and Pointers

```c
int arr[5];
int *p = arr;
```

- `arr` is a pointer to the first element
    
- Pointer arithmetic works:
    

```c
*(p + 2) = 50; // arr[2] = 50
```

- Arrays passed to functions **decay to pointers**
    

```c
void printArr(int *a, int n);
```

---

## 4. Multidimensional Arrays

```c
int mat[3][4]; // 3 rows, 4 columns
```

- Stored row-major order
    
- Access: `mat[i][j]`
    
- Memory layout:
    

```
mat[0][0], mat[0][1], mat[0][2], mat[0][3], mat[1][0], ...
```

### Example

```c
for(int i=0;i<3;i++) {
  for(int j=0;j<4;j++) {
    mat[i][j] = i*j;
  }
}
```

---

## 5. Array Operations

- Iteration using loops (`for`, `while`)
    
- Summing elements
    
- Finding min/max
    
- Sorting (selection, insertion, bubble, quicksort)
    
- Searching (linear, binary)
    

### Example: Sum of array

```c
int sum = 0;
for(int i=0;i<10;i++) sum += arr[i];
```

---

## 6. Parallel Arrays

- Multiple arrays that are logically related
    

```c
char names[5][20];
int ages[5];
```

- `names[i]` corresponds to `ages[i]`
    
- Common in student exercises
    

---

## 7. Arrays as Function Arguments

- Array decays to pointer
    
- Must also pass size
    

```c
void processArray(int arr[], int n);
```

- For multidimensional arrays, the **inner dimension must be specified**
    

```c
void printMatrix(int mat[][4], int rows);
```

---

## 8. Common Pitfalls

- Forgetting array size when passing to function
    
- Off-by-one errors
    
- Using array after freeing dynamic allocation
    
- Mixing up row-major vs column-major
    

---

## 9. Dynamic Arrays (Brief Preview)

- Use `malloc` for runtime-determined sizes
    
- `int *arr = malloc(n * sizeof(int));`
    
- Always `free(arr);`
    
- This is covered more in **dynamic_memory.md**
    

---

## 10. Case Study from C-Code Repo

- Looping through a 2D parking grid
    
- Summing values in a hospital revenue report (from Hanly book)
    
- Demonstrates indexing, nested loops, memory access patterns
    

---

## 11. Key Takeaways

- Arrays are **memory-first constructs**
    
- Must track length explicitly
    
- Indexing beyond bounds = dangerous
    
- Arrays and pointers are closely linked
    

---

_End of arrays.md_