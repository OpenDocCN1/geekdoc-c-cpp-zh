# # IV. LIBRARY FUNCTIONS

# ## MEMORY MANAGEMENT FUNCTIONS (include file is alloc.h)

| Function | Purpose |
|---|---|
| calloc(n, size) | Allocates n multiple blocks of (n * size) bytes and initializes the memory to 0. |
| coreleft(void) | Returns a measure of RAM memory not in use. |
| farcalloc(n, size) | Allocates n multiple blocks of (n * size) bytes larger than 64K. |
| farcoreleft(void) | Returns a measure of RAM memory not in use beyond the highest allocated block. |
| farfree(*ptr) | Releases a block of memory previously allocated by farcalloc(), farmalloc(), & farrealloc() pointed by ptr. |
| farmalloc(size) | Allocates a block of (size) bytes larger than 64K. |
| farrealloc(*ptr, size) | Reallocates the size of the allocated block to size pointer by ptr previously allocated by farcalloc() / farmalloc(), copying the contents to a new location, if necessary. |
| free(*ptr) | Releases a block of memory previously allocated by calloc(), malloc(), & realloc() pointed by ptr. |
| malloc(size) | Allocates a block of (size) bytes. |
| realloc(*ptr, size) | Reallocates the size of the allocated block to size pointer by ptr previously allocated by calloc() / malloc(), copying the contents to a new location, if necessary. |

# ## INTERRUPT ENABLING / DISABLING FUNCTIONS (include file is bios.h)

| Function | Purpose |
|---|---|
| bioscom() | Used for RS-232 communications (serial I/O). |
| biosdisk() | Used for interrupt 0x13 to issue disk operations directly to the BIOS. |
| biosequip() | Used for BIOS interrupt 0x11 to return an integer describing the equipment connected to the system. |
| bioskey() | Performs various keyboard operations using BIOS interrupt 0x16. |
| biosmemory() | Used for BIOS interrupt 0x12 to return the size of RAM. |
| biosprint() | Used for BIOS interrupt 0x17 to perform various printer functions on the printer identified by port. |
| biostime() | Used for BIOS interrupt 0x1A to either read or set the BIOS timer. |

# ## TEXT MODE WINDOW FUNCTIONS (include file is conio.h)

| Function | Purpose |
|---|---|
| clrscr() | Clears the text mode window. |
| clreol() | Clears to end of line in text window. |
| cgets(char*str) | Reads a string of characters from the console and stores the string (and the string length) in the location *str. |