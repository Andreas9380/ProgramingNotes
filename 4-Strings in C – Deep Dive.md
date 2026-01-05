

Strings in C are one of the **most important and most dangerous** concepts to understand. Unlike many languages, C has **no built-in string type**. Instead, strings are built on top of **character arrays and pointers**.

A deep understanding of strings explains:

* Why buffer overflows happen
* Why `strlen` is slow
* Why memory bugs are common

---

## 1. What a String Is in C

A C string is:

> A **null-terminated array of characters** (`char`)

```c
char str[] = "Hello";
```

Memory layout:

```
'H' 'e' 'l' 'l' 'o' '\0'
```

The `\0` (null terminator) marks the end of the string.

---

## 2. Declaring Strings

### As a character array

```c
char name[20];
```

* Fixed size
* Stored on stack (if local)
* Safe if size is respected

### With initialization

```c
char msg[] = "Hello";
```

Compiler adds `\0` automatically.

---

## 3. String Literals vs Arrays

```c
char *s = "Hello";
char a[] = "Hello";
```

### Key differences

| Feature              | `char *s`        | `char a[]` |
| -------------------- | ---------------- | ---------- |
| Modifiable           | ❌ No             | ✅ Yes      |
| Stored in            | Read-only memory | Stack/heap |
| Pointer reassignment | ✅                | ❌          |

Modifying a string literal = **Undefined Behavior**.

---

## 4. Accessing Characters

```c
char c = str[0];
str[1] = 'a';
```

Characters are just small integers (ASCII values).

---

## 5. Standard String Functions (`<string.h>`)

### `strlen`

```c
size_t len = strlen(str);
```

* Counts characters until `\0`
* O(n) time

### `strcpy` / `strncpy`

```c
strcpy(dest, src);  // Dangerous if dest too small
```

Safer alternatives:

* `strncpy`
* `snprintf`

---

## 6. Comparing Strings

```c
strcmp(a, b);
```

* Returns <0, 0, or >0
* Never use `==` for strings

---

## 7. Reading Strings from Input

### Dangerous

```c
gets(buffer); // ❌ NEVER USE
```

### Safer

```c
fgets(buffer, size, stdin);
```

Always specify buffer size.

---

## 8. Strings and Functions

Strings decay to pointers when passed to functions:

```c
void printStr(char *s);
```

* Function cannot know buffer size
* Caller must manage safety

---

## 9. Dynamic Strings

```c
char *s = malloc(50);
strcpy(s, "Hello");
free(s);
```

Used when size is unknown at compile time.

---

## 10. Common String Bugs

* Missing null terminator
* Buffer overflow
* Using `strlen` inside loops
* Modifying string literals

---

## 11. Case Studies from the Repo

* License plate input handling
* File parsing line-by-line
* Manual string comparison logic

All of these reinforce careful buffer management.

---

## 12. Best Practices

✅ Always allocate one extra byte for `\0`

✅ Prefer `snprintf` over `sprintf`

✅ Pass buffer sizes explicitly

✅ Treat strings as arrays, not magic objects

---

## 13. Key Takeaway

> A C string is just memory with a convention.

Respect the convention — or C will not protect you.

---

*End of strings.md*
