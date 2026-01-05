
Data types are the **foundation of everything in C**. Unlike higher-level languages, C exposes how data is represented in memory, how much space it occupies, and how it behaves when manipulated.

If you understand data types deeply, you understand:

- Why bugs happen
    
- Why performance differs
    
- Why memory corruption exists
    

---

## 1. What a Data Type Really Is

In C, a data type defines:

1. **How many bytes** are reserved in memory
    
2. **How those bytes are interpreted** (signed, unsigned, floating)
    
3. **What operations are allowed**
    

C does _not_ protect you if you misuse a type.

---

## 2. Size of Fundamental Data Types (64-bit Systems)

> These sizes match what you implicitly rely on throughout your repository.

### Integer Types

|Type|Size|Range|
|---|---|---|
|`char`|1 byte|-128 → 127 _(or 0 → 255)_|
|`unsigned char`|1 byte|0 → 255|
|`short`|2 bytes|-32,768 → 32,767|
|`unsigned short`|2 bytes|0 → 65,535|
|`int`|4 bytes|~±2 billion|
|`unsigned int`|4 bytes|0 → ~4 billion|
|`long`|8 bytes|Very large|
|`long long`|8 bytes|Very large|

⚠️ **Important**: `char` signedness is implementation-defined.

---

## 3. Signed vs Unsigned (Very Important)

### Signed

- Can represent negative numbers
    
- Uses one bit for sign
    

### Unsigned

- Can only represent non-negative numbers
    
- Larger positive range
    

### Common Bug Example

```c
int i = -1;
unsigned int u = 1;

if (i < u) {
    // FALSE – because i is converted to unsigned
}
```

**Lesson**: Avoid mixing signed and unsigned values.

---

## 4. Integer Overflow (Undefined vs Defined)

### Signed overflow

```c
int x = INT_MAX;
x = x + 1;  // ❌ Undefined Behavior
```

### Unsigned overflow

```c
unsigned int x = UINT_MAX;
x = x + 1;  // ✅ Wraps to 0
```

Your repo implicitly avoids relying on overflow — this is good practice.

---

## 5. Floating-Point Types

|Type|Size|Precision|
|---|---|---|
|`float`|4 bytes|~6 digits|
|`double`|8 bytes|~15 digits|
|`long double`|16 bytes|Platform-dependent|

### Floating-Point Reality

```c
double x = 0.1 + 0.2;
printf("%f", x); // Not exactly 0.3
```

**Lesson**: Floating-point numbers are approximations.

---

## 6. Boolean Type

C has no native boolean keyword (historically).

```c
#include <stdbool.h>
bool done = false;
```

Internally:

- Stored as `unsigned char`
    
- 0 = false
    
- Non-zero = true
    

Used extensively in your code for:

- Flags
    
- State tracking
    

---

## 7. Characters and ASCII

A `char` is just a small integer.

```c
char c = 'A';
printf("%d", c); // 65
```

This is why:

- Strings are `char[]`
    
- Character math works
    

---

## 8. sizeof Operator

`sizeof` returns the size **in bytes**.

```c
sizeof(int);        // 4
sizeof(char);       // 1
sizeof(double);     // 8
```

### Arrays vs Pointers

```c
int arr[10];
int *p = arr;

sizeof(arr); // 40
sizeof(p);   // 8
```

This distinction appears repeatedly in your repository.

---

## 9. Type Conversion (Casting)

### Implicit conversion

```c
int x = 3;
double y = x; // OK
```

### Explicit conversion

```c
double d = 3.14;
int i = (int)d; // Truncates
```

Casting does **not** change memory — only interpretation.

---

## 10. const and Volatile

### const

```c
const int x = 10;
```

- Prevents modification
    
- Does NOT guarantee immutability at machine level
    

### volatile

Used rarely, but important for:

- Hardware registers
    
- Multithreading
    

---

## 11. Data Types in Memory

Memory is linear:

```
| byte | byte | byte | byte | ... |
```

Data types simply define **how many bytes** and **how to interpret them**.

This explains:

- Pointer arithmetic
    
- Struct layout
    
- Buffer overflows
    

---

## 12. Best Practices (Exam & Real World)

✅ Use `int` unless size matters

✅ Use `size_t` for sizes

✅ Avoid mixing signed/unsigned

✅ Never rely on overflow

✅ Always know how many bytes you allocate

---

## 13. Key Takeaway

> C does not understand "numbers" — it understands **bytes and rules**.

Once you internalize this, the rest of C becomes logical instead of scary.

---

_End of data_types.md_