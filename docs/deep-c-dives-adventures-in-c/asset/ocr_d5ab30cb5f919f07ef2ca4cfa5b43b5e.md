That is, the fundamental reason for types in C is to determine the type of operation appropriate for the data.

Type determines how operators act and this is always true, no matter how much we elaborate the idea of type.

You could also add that, in C, type also determines how many bits are involved in the operation but this is more obvious – well it is to a C programmer...

# Data Representation

Data representation is a key emphasis of C as opposed to other languages which try to hide how they represent data. The trend in ever higher-level languages is to abstract away from the underlying bits and encourage the user to think in terms of objects that they can use without knowing how they work.

We have seen that in C it is the bit sequence and what it represents that is important. In other languages bits, representations and their limitations are hidden. For example, JavaScript just implements a number object and handles the distinction between integers and floats under the covers. Python has integers with unlimited precision so you never need ask what is the range of a Python integer. C on the other hand insists that you know how the data is represented. It has different sizes of integers and even has unsigned integers and you are expected to know how these work and how they relate to one another. More accurately, if you don’t understand the data representation in use you will find it harder to write correct code.

It is important to remember that, while the machine and C may offer a range of operations, which operations make sense is entirely dependent on what the bits are currently taken to represent.

This leads on to the interesting question of why a byte in C is called “char” and not “byte”? The reason is that back in the early days a char was intended to hold enough bits to represent all of the text characters the machine needed to work with. As most machines worked with ASCII, a seven-bit code, most often char was defined as being eight-bit to allow for some additional characters. Notice that right from this starting point it is clear that C wants you to have an interpretation for the bits it stores. You can add two chars together, but in this case you are supposed to think of them as eight-bit integers. You can also set all of the bits to one and then you are better thinking of them as light states.

In all cases we take a bunch of bits and combine them with another bunch of bits using an operator and the question is does the resulting bunch of bits make any sense.