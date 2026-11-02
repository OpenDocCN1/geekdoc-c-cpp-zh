letter b) for manipulating binary files. The binary modes are used in Sections 11.5–11.9 when we introduce random-access files.

| Mode | Description |
|---|---|
| `r` | Open an existing file for reading. |
| `w` | Create a file for writing. If the file already exists, discard the current contents. |
| `a` | Open or create a file for writing at the end of the file—i.e., write operations append data to the file. |
| `r+` | Open an existing file for update (reading and writing). |
| `w+` | Create a file for reading and writing. If the file already exists, discard the current contents. |
| `a+` | Open or create a file for reading and updating; all writing is done at the end of the file—i.e., write operations append data to the file. |
| `rb` | Open an existing file for reading in binary mode. |
| `wb` | Create a file for writing in binary mode. If the file already exists, discard the current contents. |
| `ab` | Append: open or create a file for writing at the end of the file in binary mode. |
| `rb+` | Open an existing file for update (reading and writing) in binary mode. |
| `wb+` | Create a file for update in binary mode. If the file already exists, discard the current contents. |
| `ab+` | Open or create a file for update in binary mode; writing is done at the end of the file. |

**Fig. 11.5**  File opening modes.

# C11 Exclusive Write Mode

In addition, C11 provides exclusive write mode, which you indicate by adding an x to the end of the w, w+, or wb+ modes. In exclusive write mode, fopen will fail if the file already exists or cannot be created. If opening a file in exclusive write mode is successful and the underlying system supports exclusive file access, then only your program can access the file while it’s open. (Some compilers and platforms do not support exclusive write mode.) If an error occurs while opening a file in any mode, fopen returns NULL.

> **Common Programming Error 11.3**
> 
> *Opening a nonexistent file for reading is an error.*

![](bbox=[0.16, 0.748, 0.216, 0.788])

> **Common Programming Error 11.4**
> 
> *Opening a file for reading or writing without having been granted the appropriate access rights to the file (this is operating-system dependent) is an error.*

![](bbox=[0.16, 0.818, 0.216, 0.859])

> **Common Programming Error 11.5**
> 
> *Opening a file for writing when no space is available is a runtime error.*

![](bbox=[0.16, 0.889, 0.216, 0.93])