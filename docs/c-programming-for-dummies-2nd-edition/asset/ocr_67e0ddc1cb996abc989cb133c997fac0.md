> I can reason why a pointer is called a pointer: It points at something, a location in memory. The problem with this description is that most pedants explain how a pointer works by uttering the phrase, “A pointer points . . .” This explanation is just wrong. It confuses the issue.
> 
> Adding to the name confusion is the fact that pointers have two personalities. One side is a variable that holds a memory location, an address. The other side reveals the value at that address. In this way, the pointer should be called a peeker. This chapter helps straighten out the confusion.

![](bbox=[0.05, 0.22, 0.95, 0.35])

# Sizing Up Variable Storage

Digital storage is measured in bytes. All the information stored inside memory is simply a mass of data, bits piled upon bits, bytes upon bytes. It's up to the software to make sense of it all.

# Understanding variable storage

In C, data is categorized by storage type (char, int, float, or double) and further classified by keyword (long, short, signed, or unsigned). Despite the chaos inside memory, your program's storage is organized into these values, ready for use in your code.

Inside a running program, a variable is described by these attributes:

+   - Name
+   - Type
+   - Value
+   - Size
+   - Location