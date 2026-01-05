

Functions are how C programs are **structured, reused, and reasoned about**. They also define how the **stack**, **parameters**, and **return values** work at runtime.

Understanding functions deeply explains:

- Why some bugs only appear after a function returns
    
- How recursion works
    
- How performance and memory usage are affected
    

---

## 1. What a Function Is

A function is a **named block of code** with:

- Parameters (inputs)
    
- A return value (output)
    
- Its own stack frame
    

```c
int add(int a, int b) {
    return a + b;
}
```

---

## 2. Function Declarations vs Definitions

### Declaration (prototype)

```c
int add(int a, int b);
```

- Tells the compiler the function exists
    
- Enables type checking before use
    

### Definition

```c
int add(int a, int b) {
    return a + b;
}
```

Used throughout your repo to split `.h` and `.c` files.

---

## 3. Parameters Are Passed by Value

```c
void f(int x) {
    x = 10;
}
```

Calling `f(a)` does **not** modify `a`.

### Why?

- Parameters are copied onto the stack
    

---

## 4. Simulating Pass-by-Reference with Pointers

```c
void f(int *x) {
    *x = 10;
}
```

Now the caller’s variable **is modified**.

This pattern is used extensively in your codebase.

---

## 5. The Stack Frame (Critical Concept)

Each function call creates a **stack frame** containing:

- Parameters
    
- Local variables
    
- Return address
    

```c
void g() {
    int x = 5;
}
```

When `g()` returns, `x` is destroyed.

---

## 6. Returning Values

```c
int square(int x) {
    return x * x;
}
```

- Returned value is copied to caller
    
- Returning pointers requires caution
    

### Dangerous Return

```c
int *bad() {
    int x = 5;
    return &x; // ❌ dangling pointer
}
```

---

## 7. Returning Structs

```c
typedef struct {
    int x;
    int y;
} Point;

Point makePoint() {
    Point p = {1, 2};
    return p; // safe
}
```

C copies the struct.

---

## 8. Recursive Functions

```c
int factorial(int n) {
    if (n == 0) return 1;
    return n * factorial(n - 1);
}
```

Each recursive call creates a new stack frame.

⚠️ Risk: stack overflow if recursion is too deep.

---

## 9. Variable Scope

### Local variables

```c
void f() {
    int x;
}
```

- Exist only inside the function
    

### Global variables

```c
int counter;
```

- Exist for entire program lifetime
    
- Used sparingly in your repo
    

---

## 10. Static Variables in Functions

```c
void counter() {
    static int x = 0;
    x++;
}
```

- Initialized once
    
- Retain value between calls
    

---

## 11. Function Pointers (Intro)

```c
int (*fp)(int, int) = add;
```

Used for:

- Callbacks
    
- Strategy patterns
    
- Event handling
    

---

## 12. Functions in Your Repository

Examples include:

- Utility helpers
    
- Data processing functions
    
- Algorithmic functions
    

Demonstrates:

- Clean modular design
    
- Header/source separation
    

---

## 13. Common Function Bugs

- Returning address of local variable
    
- Forgetting function prototypes
    
- Mismatched parameter types
    
- Overusing globals
    

---

## 14. Best Practices

✅ Keep functions small

✅ One responsibility per function

✅ Pass pointers only when necessary

✅ Declare before use

---

## 15. Key Takeaway

> Functions define **control flow, memory lifetime, and structure**.

If you understand the stack, you understand functions.

---

_End of functions.md_