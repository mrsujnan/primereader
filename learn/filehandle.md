# File Handling in C

File handling in C is a fundamental concept that allows programs to read, write, and manipulate files stored on disk. Below is a comprehensive guide to file handling in C, including functions, modes, and examples.

---

## 1. File Operations in C

The main file operations in C are:

- **Create a file**
- **Open a file**
- **Read from a file**
- **Write to a file**
- **Close a file**

These operations are performed using standard I/O functions available in the `stdio.h` library.

---

## 2. File Pointers

- A file is managed in C through a `FILE` pointer, defined in `stdio.h`.
  ```c
  FILE *filePointer;
  ```
- The `FILE` pointer keeps track of the file's status, including its position and access mode.

---

## 3. File Modes

File modes specify how a file is accessed. Common modes include:

| Mode | Description                                                               |
| ---- | ------------------------------------------------------------------------- |
| `r`  | Open a file for reading.                                                  |
| `w`  | Open a file for writing. Creates a new file or truncates an existing one. |
| `a`  | Open a file for appending. Creates the file if it doesn’t exist.          |
| `r+` | Open a file for reading and writing.                                      |
| `w+` | Open a file for reading and writing. Truncates the file if it exists.     |
| `a+` | Open a file for reading and appending.                                    |

---

## 4. Basic File Handling Functions

### a. `fopen()`

Opens a file and returns a `FILE` pointer.

```c
FILE *fopen(const char *filename, const char *mode);
```

**Example:**

```c
FILE *file = fopen("example.txt", "r");
if (file == NULL) {
    printf("Error opening file!\n");
}
```

### b. `fclose()`

Closes an open file.

```c
int fclose(FILE *stream);
```

**Example:**

```c
fclose(file);
```

### c. `fprintf()`

Writes formatted output to a file.

```c
int fprintf(FILE *stream, const char *format, ...);
```

**Example:**

```c
fprintf(file, "Hello, World!\n");
```

### d. `fscanf()`

Reads formatted input from a file.

```c
int fscanf(FILE *stream, const char *format, ...);
```

**Example:**

```c
fscanf(file, "%d", &number);
```

### e. `fgetc()`

Reads a single character from a file.

```c
int fgetc(FILE *stream);
```

**Example:**

```c
char ch = fgetc(file);
```

### f. `fputc()`

Writes a single character to a file.

```c
int fputc(int char, FILE *stream);
```

**Example:**

```c
fputc('A', file);
```

### g. `fgets()`

Reads a string from a file.

```c
char *fgets(char *str, int n, FILE *stream);
```

**Example:**

```c
fgets(buffer, 100, file);
```

### h. `fputs()`

Writes a string to a file.

```c
int fputs(const char *str, FILE *stream);
```

**Example:**

```c
fputs("Hello, file!", file);
```

### i. `fseek()`

Moves the file pointer to a specific location in the file.

```c
int fseek(FILE *stream, long offset, int origin);
```

`origin` can be:

- `SEEK_SET`: Beginning of the file
- `SEEK_CUR`: Current position of the file pointer
- `SEEK_END`: End of the file

**Example:**

```c
fseek(file, 0, SEEK_SET);
```

### j. `ftell()`

Returns the current position of the file pointer.

```c
long ftell(FILE *stream);
```

**Example:**

```c
long position = ftell(file);
```

### k. `rewind()`

Resets the file pointer to the beginning of the file.

```c
void rewind(FILE *stream);
```

**Example:**

```c
rewind(file);
```

### l. `feof()`

Checks if the end of a file has been reached.

```c
int feof(FILE *stream);
```

**Example:**

```c
if (feof(file)) {
    printf("End of file reached.\n");
}
```

---

## 5. Example: Writing and Reading a File

### Writing to a File

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "w");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    fprintf(file, "Hello, File Handling in C!\n");
    fclose(file);
    return 0;
}
```

### Reading from a File

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("example.txt", "r");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    char buffer[100];
    while (fgets(buffer, 100, file) != NULL) {
        printf("%s", buffer);
    }

    fclose(file);
    return 0;
}
```

---

## 6. Error Handling in File Operations

Always check for errors when working with files:

```c
FILE *file = fopen("nonexistent.txt", "r");
if (file == NULL) {
    perror("Error opening file");
    return 1;
}
```

- Use `perror()` to print system-defined error messages.

---

## 7. Binary File Handling

Binary files store data in a non-human-readable format.

### Writing Binary Data

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("binary.dat", "wb");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    int numbers[] = {1, 2, 3, 4, 5};
    fwrite(numbers, sizeof(int), 5, file);
    fclose(file);
    return 0;
}
```

### Reading Binary Data

```c
#include <stdio.h>

int main() {
    FILE *file = fopen("binary.dat", "rb");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    int numbers[5];
    fread(numbers, sizeof(int), 5, file);

    for (int i = 0; i < 5; i++) {
        printf("%d ", numbers[i]);
    }

    fclose(file);
    return 0;
}
```

---

## 8. Common Mistakes to Avoid

- Forgetting to close a file.
- Not checking if the file was opened successfully.
- Using incorrect file modes.
- Accessing the file pointer after closing the file.

---

## 9. Tips for File Handling

- Always validate file operations with error checking.
- Use binary mode for non-text data to avoid encoding issues.
- Utilize `fseek` and `ftell` for efficient file pointer navigation.

---

This guide covers the fundamental aspects of file handling in C. By understanding these concepts and practicing with examples, you can efficiently manage files in your C programs.
