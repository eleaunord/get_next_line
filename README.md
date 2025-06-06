# get\_next\_line

> Reading a line from a file descriptor is far too tedious. This project aims to fix that.

## 📄 Project Overview

**`get_next_line`** is a 42 Common Core project that focuses on building a function capable of reading text line by line from a file descriptor. The function handles multiple successive calls, returning each line one at a time until the end of the file or an error.

This project reinforces low-level C programming concepts, especially static variables, memory management, file I/O, and buffering strategies.

## Function Prototype

```c
char *get_next_line(int fd);
```

## 🎯 Project Goals

* Handle line-by-line file reading efficiently.
* Manage buffers and partial reads correctly.
* Understand and use static variables.
* Write clean, memory-safe C code without external dependencies.

## ⚙️ Features

* Reads from file descriptors line by line.
* Each line includes the newline character if one exists.
* Returns `NULL` at end-of-file or on error.
* Supports arbitrary buffer sizes via `-D BUFFER_SIZE=n`.

## 🧠 What I Learned

### Static Variables

* Learned how to persist data between function calls using static variables.
* Used static memory to keep track of leftover data that wasn’t returned during the previous read.

### Memory Management

* Understood the importance of managing heap memory precisely in constrained environments.
* Avoided memory leaks and segmentation faults by allocating and freeing buffers thoughtfully.

### File Descriptor Handling

* Realized that reading from different file descriptors requires isolated states.
* Learned how to structure code to handle multiple FDs simultaneously in the bonus version.

### Line and Buffer Logic

* Understood the balance between reading enough and not reading too much.
* Implemented logic to stop reading as soon as a newline is found.

## 😓 Challenges Faced

### Partial Reads and Leftovers

* **Problem:** Handling cases where the newline wasn’t in the current read buffer.
* **Solution:** Stored leftover characters in a static buffer and appended future reads to it.

### BUFFER\_SIZE Edge Cases

* **Problem:** The function had to work with a very small (e.g., 1) or very large (e.g., 10000) buffer.
* **Solution:** Carefully tested all edge cases and avoided assumptions about buffer size.

### Bonus: Multiple File Descriptors

* **Problem:** Maintaining an independent state per file descriptor.
* **Solution:** Created a data structure indexed by FD and handled cleanup when needed.

## 🧪 Compilation

You can compile the project with:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c main.c
```

Replace `main.c` with your test file.

## Testing Tips

* Vary `BUFFER_SIZE`: try 1, 10, 10000
* Test with files ending with and without `\n`
* Feed multiple file descriptors simultaneously (bonus)
* Include edge cases: empty files, long lines, stdin input

## Final Thoughts

`get_next_line` was a challenging but rewarding project that deepened my understanding of low-level file I/O in C. It taught me how to manage state across function calls, handle buffers efficiently, and write memory-safe code.
