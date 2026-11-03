variables while the uninitialized data area stores all the uninitialized static and global variables. The reason for division of this area is that all uninitialized variables can be collectively assigned value zero. The size of data area is also fixed and does not change during run time.

| Code | Code of the program |
|---|---|
| Initialized Data | Initialized static variables
Initialized global variables |
| Uninitialized Data | Uninitialized static variables
Uninitialized global variables |
| Heap | Dynamically allocated memory |
|  |  |
| Stack | Initialized and uninitialized automatic variables |

# Memory during execution of the program

Heap: This area is used for dynamically allocated memory. It is the responsibility of the program to allocate memory from the heap. The size of this area is dynamic i.e. it may change during run time

Stack: Automatic variables are stored in this area. The size of this area keeps on changing during time.

The following table summarizes all the features of storage classes-

| Keyword | Place of declaration | Lifetime | Scope | Initial Value | Place of storage | Linkage | Initiali |
|---|---|---|---|---|---|---|---|
| auto (or none) | Inside Function /Block | Function /Block | Function /Block | Garbage | Memory (stack) | None | Constant Variable |
| register | Inside Function /Block | Function /Block | Function /Block | Garbage | Registers | None | Constant Variable |
| static (local) | Inside Function /Block | Program | Function / Block | Zero | Memory (data area) | None | Const |
| (none) | Outside function (Definition of external | Program | Definition to end of file (can be shared in other files | Zero | Memory (data area) | External | Const |