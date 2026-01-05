
Structs are how C models **real-world data**. They let you group related values into a single unit and are the foundation of most non-trivial programs.

This file explains **how structs live in memory**, how they interact with pointers, and how `typedef` improves readability.

---

## 1. What a struct Is

A `struct` groups multiple variables under one name.

```c
struct Person {
    int id;
    char name[50];
    int age;
};
```

This defines a **new data layout**, not a variable.

---

## 2. Declaring Struct Variables

```c
struct Person p1;
```

Or with initialization:

```c
struct Person p2 = {1, "Lukas", 22};
```

---

## 3. typedef – Making Structs Usable

Without `typedef`:

```c
struct Person p;
```

With `typedef`:

```c
typedef struct {
    int id;
    char name[50];
} Person;

Person p;
```

This style is used throughout your repository.

---

## 4. Memory Layout and Padding

Struct members are stored **sequentially**, but padding may be added for alignment.

Example:

```c
typedef struct {
    char c;
    int i;
} Example;
```

Layout (64-bit):

```
| c | pad | pad | pad | i | i | i | i |
```

Padding improves performance but increases size.

---

## 5. sizeof and Structs

```c
sizeof(Example); // likely 8, not 5
```

Never assume struct size — always use `sizeof`.

---

## 6. Accessing Struct Members

```c
Person p;
p.id = 10;
```

With pointers:

```c
Person *ptr = &p;
ptr->id = 10;
```

`->` is shorthand for `(*ptr).id`.

---

## 7. Structs and Functions

### Passing by value

```c
void print(Person p);
```

- Copies entire struct
    
- Can be expensive for large structs
    

### Passing by pointer

```c
void update(Person *p);
```

- Efficient
    
- Allows modification
    

Used extensively in your code.

---

## 8. Arrays of Structs

```c
Person people[100];
```

Common use cases:

- Databases
    
- Tables
    
- Records
    

Access:

```c
people[i].age;
```

---

## 9. Dynamic Struct Allocation

```c
Person *p = malloc(sizeof *p);
```

Must be freed:

```c
free(p);
```

Ownership rules apply.

---

## 10. Nested Structs

```c
typedef struct {
    int x, y;
} Point;

typedef struct {
    Point pos;
    int health;
} Player;
```

Encourages clean modeling.

---

## 11. Structs vs Arrays

- Arrays: homogeneous data
    
- Structs: heterogeneous data
    

Most programs use both together.

---

## 12. Structs in Your Repository

Used for:

- State containers
    
- Domain models
    
- File records
    

Demonstrates proper modular design.

---

## 13. Common Struct Mistakes

- Forgetting padding effects
    
- Copying large structs unintentionally
    
- Using uninitialized members
    

---

## 14. Best Practices

✅ Use `typedef` for readability

✅ Pass structs by pointer if large

✅ Initialize all members

✅ Use `sizeof(structType)`

---

## 15. Key Takeaway

> Structs turn raw memory into meaningful data.

Understanding their layout is essential for safe C programming.

---

_End of structs_and_typedef.md_