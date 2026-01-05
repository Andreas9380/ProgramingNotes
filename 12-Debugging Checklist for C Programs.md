

This file is a **practical, step-by-step debugging guide** you can use during assignments, exams, and real projects. When something breaks, you don’t guess — you walk this list.

---

## 1. First Rule: Assume the Bug Is Yours

C almost never fails randomly.  
If something is wrong, assume:

- Memory misuse
    
- Lifetime error
    
- Undefined behavior
    

This mindset saves time.

---

## 2. Compile With Maximum Warnings

Always compile with:

```bash
gcc -Wall -Wextra -Wshadow -Wconversion -pedantic
```

Rules:

- Fix **every warning**
    
- Warnings are bugs in disguise
    

---

## 3. Check All Assumptions

For each variable, ask:

- Is it initialized?
    
- Is it in scope?
    
- Does it still exist?
    
- Is its type what I think it is?
    

Most bugs fail one of these.

---

## 4. Memory Ownership Audit

For every pointer, answer:

|Question|Answer|
|---|---|
|Who allocated it?||
|Who frees it?||
|When is it freed?||
|Is it used after free?||

If you can’t answer → bug likely exists.

---

## 5. Stack vs Heap Check

Common failures:

- Returning address of local variable
    
- Storing stack addresses globally
    

```c
int *bad() {
    int x = 5;
    return &x; // BUG
}
```

Fix: allocate on heap or pass pointer in.

---

## 6. Array Boundaries

Check every array access:

- Is index >= 0?
    
- Is index < array length?
    

Remember:

> C will NOT stop you.

---

## 7. String Rules Verification

For every string:

- Is it null-terminated?
    
- Is the buffer large enough?
    
- Are you modifying a literal?
    

```c
char *s = "hi";
s[0] = 'H'; // BUG
```

---

## 8. Pointer Validity Test

Before dereferencing:

```c
if (p == NULL) {
    // handle error
}
```

Check that:

- Pointer was initialized
    
- Points to valid memory
    
- Points to correct type
    

---

## 9. Function Call Sanity

Verify:

- Function prototype matches definition
    
- Argument order is correct
    
- Pointer arguments are valid
    

Many bugs are mismatched expectations.

---

## 10. Control Flow Inspection

Look for:

- Missing `return`
    
- Missing `break` in `switch`
    
- Wrong loop conditions
    

```c
while (i = 0) { } // BUG
```

---

## 11. Print Debugging (Done Right)

Print:

- Pointer addresses (`%p`)
    
- Values before and after change
    

```c
printf("p=%p value=%d\n", (void*)p, *p);
```

---

## 12. Use Tools Early

### Valgrind

Finds:

- Leaks
    
- Invalid reads/writes
    

### AddressSanitizer

Compile with:

```bash
-fsanitize=address
```

---

## 13. Reduce the Problem

If stuck:

- Comment out code
    
- Isolate smallest failing example
    
- Test functions independently
    

Small programs are easier to reason about.

---

## 14. Mental Model Check

Ask:

1. Where is this memory?
    
2. Who owns it?
    
3. When does it die?
    
4. Is behavior defined?
    

If any answer is unclear → bug lives there.

---

## 15. Exam-Specific Advice

In exams:

- UB is often intentional
    
- Pointer errors are subtle
    
- Correct-looking code may still be wrong
    

Slow down and simulate execution.

---

## 16. Final Rule

> Debugging C is not guessing — it is **elimination**.

Follow the checklist. Every time.

---

_End of debugging_checklist.md_