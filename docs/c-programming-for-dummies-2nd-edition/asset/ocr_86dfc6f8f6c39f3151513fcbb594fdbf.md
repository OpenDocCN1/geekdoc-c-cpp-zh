The source code from Listing 19-4 deals with a single char variable and not an array. Therefore, the pointer initialization in Line 9 requires the & prefix. Don't forget it!

Line 12 in this code contains the booger (*pa)++. It looks similar to *pa++, but it's definitely not. Unlike *pa++, which peeks at a value and then increments the pointer, the (*pa)++ construction increments a value being peeked at; the pointer's address is unchanged.

# Exercise 19-10, Edit, build, and run a new program by using the source code from Listing 19-4,

The (*pa)++ operation works, thanks to the parentheses. The program fetches the value represented by *pa first, and then that value is incremented. The pointer variable, pa, isn't affected by the operation; pa still holds the address of char variable alpha.

To help avoid confusion on this topic, I offer Table 19-1, which explains the various cryptic pointer/peek er notation doodads.

# TABLE 19-1 Pointers and Peekers In and Out of Parentheses

| Expression | Address p | Value *p |
|---|---|---|
| *p++ | Incremented after the value is read | Unchanged |
| *(p++) | Incremented after the value is read | Unchanged |
| (*p)++ | Unchanged | Incremented after it's read |
| *++p | Incremented before the value is read | Unchanged |
| *(++p) | Incremented before the value is read | Unchanged |
| ++*p | Unchanged | Incremented before it's read |
| ++(*p) | Unchanged | Incremented before it's read |

Use Table 19-1 to help you decipher code as well as get the correct format for what you need done with a pointer. If the pointer notation you see or want doesn't appear in Table 19-1, it's either not possible or not a pointer. For example, the expressions p+++ and p+++ may look like they belong in Table 19-1, but they're not pointers. (In fact, they're not defined as valid expressions in C.)