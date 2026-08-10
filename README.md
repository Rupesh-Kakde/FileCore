# 📁 FileCore — Low-Level File Management System in C

## ▸ Overview

**FileCore** is a command-line based, memory-resident **low-level file management system implemented in C**.

The project is designed to demonstrate how files can be managed internally using system-level data structures such as **Inodes, File Tables, User File Descriptor Tables (UFDT), UAREA, file descriptors, memory buffers, and linked-list based inode management**.

FileCore provides an interactive shell-like interface that allows users to create, write, read, inspect, list, and delete files while maintaining their metadata, permissions, offsets, and dynamically allocated storage in memory.

---

## ▸ Purpose of the Project

The primary purpose of FileCore is to gain practical understanding of **Operating System and system programming concepts** by implementing a simplified file-management environment from scratch in C.

The project focuses on:

- Understanding inode-based file management
- Managing file descriptors and file-table entries
- Working with UAREA and UFDT
- Managing file permissions
- Handling file metadata
- Managing read and write offsets
- Using dynamic memory allocation
- Implementing linked-list based resource management
- Designing a command-driven system interface
- Handling errors and resource constraints

---

## ▸ Key Concepts Used

### 🔹 Boot Block

The Boot Block stores basic information related to the initialization of the FileCore environment.

### 🔹 Super Block

The Super Block maintains overall inode information, including:

- Total number of inodes
- Number of free inodes

### 🔹 Inode

Each file is represented using an inode containing information such as:

- File name
- Inode number
- File size
- Actual file size
- File type
- Reference count
- Permissions
- Data buffer
- Link to the next inode

The inodes are maintained using a **linked-list based structure**.

### 🔹 File Table

The File Table maintains information associated with a file entry, including:

- Read offset
- Write offset
- Access mode
- Pointer to the associated inode

### 🔹 UAREA and UFDT

The **User Area (UAREA)** maintains the **User File Descriptor Table (UFDT)**, which associates file descriptors with their corresponding file-table entries.

### 🔹 Dynamic Memory Allocation

Memory is dynamically allocated for:

- Inodes
- File-table entries
- File data buffers

### 🔹 Linked List

A linked list is used to maintain and manage the collection of inodes.

### 🔹 Command-Line Interface

FileCore provides an interactive command interpreter through which users can execute file-management operations.

---

## ▸ Features

### 📄 File Management

- Create files using `creat`
- List files using `ls`
- Display detailed file information using `ls -a`
- Inspect file metadata using `stat`
- Delete files using `unlink`

### ✍️ File Operations

- Write data using `write`
- Read data using `read`
- Maintain separate read and write offsets
- Track actual file size

### 🔐 Permission Management

FileCore supports:

```text
1 → Read
2 → Write
3 → Read + Write
```

Permission checks are performed before read and write operations.

### 🧠 Metadata Management

The system maintains:

- Inode number
- File size
- Actual file size
- File type
- Reference count
- Permissions

### ⚠️ Error Handling

Custom error codes are used to handle conditions such as:

- Invalid parameters
- No free inodes
- Duplicate file names
- File not found
- Permission denied
- Insufficient storage
- Insufficient data
- Maximum open-file limit

---

## ▸ Architecture

```text
                         FileCore
                            │
                            ▼
                  Command-Line Interface
                            │
                            ▼
                    Command Interpreter
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
        File Operations  File Descriptors  Metadata
             │              │              │
             ▼              ▼              ▼
           Inode         File Table     Super Block
             │              │
             └───────┬──────┘
                     ▼
                    UFDT
                     │
                     ▼
             Dynamic Data Buffer
```

---

## ▸ Project Structure

```text
📁 FileCore
│
├── 📁 src
│   └── filecore.c
│
├── README.md
├── LICENSE
└── .gitignore
```

### File Description

| File / Folder | Description |
|---|---|
| `src/filecore.c` | Main C source containing the complete FileCore implementation |
| `README.md` | Project documentation |
| `LICENSE` | Project license |
| `.gitignore` | Files excluded from Git tracking |

---

## ▸ How to Run

### Step 1: Clone the Repository

```bash
git clone https://github.com/Rupesh-Kakde/FileCore.git
```

### Step 2: Navigate to the Project

```bash
cd FileCore
```

### Step 3: Compile

```bash
gcc src/filecore.c -o filecore
```

### Step 4: Run

#### Linux / macOS

```bash
./filecore
```

#### Windows

```powershell
.\filecore.exe
```

---

## ▸ How to Use

After starting the program, the FileCore command prompt appears:

```text
FileCore : >
```

### Available Commands

| Command | Description |
|---|---|
| `help` | Display available commands |
| `man Command` | Display manual information for a command |
| `creat FileName Permission` | Create a new file |
| `ls` | List all existing files |
| `ls -a` | Display detailed file information |
| `write FD` | Write data into a file |
| `read FD Size` | Read specified bytes from a file |
| `stat FileName` | Display file metadata |
| `unlink FileName` | Delete an existing file |
| `clear` | Clear the terminal |
| `exit` | Terminate FileCore |

---

## ▸ Permission Values

When creating a file, the permission value determines the allowed operation:

```text
1 → Read
2 → Write
3 → Read + Write
```

### Example

```text
creat demo.txt 3
```

This creates `demo.txt` with **Read + Write** permission.

---

## ▸ Example Usage

### Create a File

```text
FileCore : > creat demo.txt 3
File Successfully created with FD : 3
```

### List Files

```text
FileCore : > ls

---------------- FileCore Files Information -----------------

demo.txt
```

### Write Data

```text
FileCore : > write 3

Enter the data that you want to write into the file
Hello FileCore

14 Bytes gets successfully written into the file
```

### Read Data

```text
FileCore : > read 3 14

Read operation is successful
Data from file is :
Hello FileCore
```

### Display File Metadata

```text
FileCore : > stat demo.txt

File name : demo.txt
Inode number : 1
File size : 50
Actual file size : 14
Reference count : 1
File Permission : Read + Write
File type : Regular file
```

### Delete File

```text
FileCore : > unlink demo.txt
```

---

## ▸ Error Handling

FileCore defines custom error codes for different failure conditions:

```text
ERR_INVALID_PARAMETER
ERR_NO_INODES
ERR_FILE_ALREADY_EXIST
ERR_FILE_NOT_EXIST
ERR_PERMISSION_DENIED
ERR_INSUFFICIENT_SPACE
ERR_INSUFFICIENT_DATA
ERR_MAX_FILES_OPEN
```

These codes allow different file-operation failures to be identified and handled separately.

---

## ▸ System Characteristics

| Characteristic | Implementation |
|---|---|
| Programming Language | C |
| Interface | Command-Line |
| Storage Model | In-Memory |
| File Representation | Inode |
| Inode Management | Linked List |
| Descriptor Management | UFDT |
| File Management | File Table |
| Memory Management | Dynamic Allocation |
| Permissions | Read / Write / Read + Write |
| File Operations | Create / Read / Write / Stat / Unlink |
| Persistence | No — memory only |

---

## ▸ Important Notes

- FileCore stores file data in dynamically allocated memory.
- Data is not persisted to physical disk.
- All files and their contents are lost when the program terminates.
- The current implementation uses fixed limits for inodes, open files, and file size.
- File descriptors are used for file operations.
- Read and write operations maintain independent file offsets.
- File metadata is maintained through inode structures.

---

## ▸ Real-World Relevance

The concepts implemented in FileCore are closely related to fundamental areas of:

- Operating Systems
- System Programming
- File Management
- Memory Management
- Data Structures
- Low-Level C Programming

The project provides practical exposure to how multiple system-level data structures can work together to manage file resources.

---

## ▸ Learning Outcomes

Through the development of FileCore, I gained practical experience in:

- Designing system-level applications in C
- Understanding inode-based file management
- Working with file descriptors and file tables
- Implementing linked-list based resource management
- Working extensively with pointers and structures
- Managing dynamically allocated memory
- Implementing file permissions
- Managing read/write offsets
- Handling system constraints and errors
- Designing an interactive command interpreter
- Translating Operating System concepts into a working implementation

---

## ▸ Future Enhancements

Possible future improvements include:

- Open and close file semantics
- Seek operation
- Persistent storage
- Directory management
- Hierarchical directory structure
- Improved memory and resource cleanup
- Extended permission handling
- Additional file-management commands
- Enhanced command history and shell interaction

---

## ▸ Author

**Rupesh Suresh Kakde**

MCS — Computer Science

---

## ▸ Project Status

🟢 **Core implementation completed and tested**

FileCore currently supports the fundamental file-management workflow:

```text
Create
  ↓
List
  ↓
Write
  ↓
Read
  ↓
Inspect Metadata
  ↓
Delete
```

The project is designed as an educational system-programming implementation and can be extended with additional file-management and storage capabilities.