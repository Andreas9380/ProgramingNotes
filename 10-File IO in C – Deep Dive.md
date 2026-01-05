

File input/output (I/O) allows C programs to interact with the outside world: read data, write results, log output, and persist state. This file explains **how file I/O works**, why it is error-prone, and how to do it safely.

---

## 1. Files and Streams

In C, files are accessed via **streams**, represented by `FILE *`.

- A stream is an abstraction over:
    
    - Files on disk
        
    - Standard input/output
        
    - Pipes and devices
        

Common predefined streams:

- `stdin`
    
- `stdout`
    
- `stderr`
    

---

## 2. Opening and Closing Files

### fopen

```c
FILE *f = fopen("data.txt", "r");
if (!f) {
    perror("fopen");
    return 1;
}
```

Modes:

|Mode|Meaning|
|---|---|
|`r`|Read (file must exist)|
|`w`|Write (truncate or create)|
|`a`|Append|
|`r+`|Read/write|
|`wb`|Binary write|

### fclose

```c
fclose(f);
```

Always close files you open.

---

## 3. Character-Based I/O

### fgetc / fputc

```c
int c = fgetc(f);
if (c != EOF) {
    putchar(c);
}
```

Useful for:

- Parsers
    
- Tokenizers
    
- Character-level processing
    

---

## 4. Line-Based I/O

### fgets

```c
char buf[100];
if (fgets(buf, sizeof buf, f)) {
    printf("%s", buf);
}
```

- Reads until newline or buffer limit
    
- Includes newline if present
    
- Always null-terminates
    

Preferred over `gets` (which is removed).

---

## 5. Formatted I/O

### fprintf / fscanf

```c
fprintf(f, "%d %f\n", x, y);
```

```c
int a;
float b;
fscanf(f, "%d %f", &a, &b);
```

⚠️ `fscanf` is fragile:

- Whitespace-sensitive
    
- Hard to validate
    

---

## 6. Binary I/O

### fread / fwrite

```c
fwrite(arr, sizeof arr[0], count, f);
fread(arr, sizeof arr[0], count, f);
```

Used for:

- Struct serialization
    
- Performance
    

⚠️ Binary files are **not portable** across architectures.

---

## 7. Error Handling

Always check return values:

```c
if (ferror(f)) {
    // error occurred
}
```

Use:

- `perror()`
    
- `errno`
    

---

## 8. End-of-File Handling

```c
while ((c = fgetc(f)) != EOF) {
    // process
}
```

EOF is a **state**, not a character.

---

## 9. File Positioning

```c
fseek(f, 0, SEEK_SET);
long pos = ftell(f);
rewind(f);
```

Used for:

- Random access
    
- File parsing
    

---

## 10. Common File I/O Mistakes

- Forgetting to check `fopen`
    
- Reading past EOF
    
- Buffer overflow with `fscanf`
    
- Forgetting `fclose`
    

---

## 11. Safe File Reading Pattern

```c
char line[256];
while (fgets(line, sizeof line, f)) {
    // process line
}
```

This is the **recommended default**.

---

## 12. File I/O in Your Repository

Your exercises use file I/O to:

- Load structured input
    
- Parse values
    
- Separate logic from data
    

This builds real-world discipline.

---

## 13. Key Takeaway

> File I/O failures are **normal**, not exceptional.

Always assume:

- Files may not exist
    
- Data may be malformed
    

Defensive code wins.

---

_End of file_io.md_