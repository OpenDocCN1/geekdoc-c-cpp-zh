# # Data Types in C

All the data types defined by C are made up of units of memory called *bytes*. On most architectures a byte is built up of eight bits, each bit stores a one or a zero. These eight bits with two states contribute 256 combinations (2⁸). So an integer which takes up two bytes can store a number between 0 and 65535 (0 and 2¹⁶). Usually however, integer variables use the first bit to store whether the number is positive or negative so their value will be between −32768 and +32767.

As we mentioned, there are eight basic data types defined in the C language. Five types for storing integers of changing sizes and three types for storing *floating point* values (values with a decimal point). C does not allow for a basic data type for text. Text is built up of individual characters and characters are positioned by numbers. In the last example, we applied one of the integer types: *int*. This is the most usually used type in the C language.

The majority of data applied in computer programs is made up of the integer types, we shall talk about the floating point types a little later. In order of size, beginning with the smallest, the integer types are **char, short, int, long** and **long long**. The smaller types have the advantage of adopting less memory, the larger types obtain a performance penalty. Variables of type *int* store the largest potential integer which does not incur this performance penalty. For this reason, *int* variables can be different depending what type of computing machine you are using.

The *char* data type is commonly one byte, it is so called because they are usually used

to store single characters. The size of the other types is depending on the hardware of your computer. Most computers are “32-bit”, this refers to the size of data that they are designed for processing. On “32-bit” machines the *int* data type takes up 4 bytes (2³²). The **short** is usually smaller, the **long** can be larger or the same size as an **int** and finally the **long** is for handling very large numbers.

The type of variable you use broadly does not have a big impact on the speed or memory usage of your application. Unless you have a special need you can just use *int* variables. We will try to point out the few cases where it can be important in this chapter. A decade ago, most computing machines had 16-bit processors; this limited the size of *int* variables to 2 bytes. At the time, **short** variables were commonly also 2 bytes and **long** would be 4 bytes. Nowadays, with 32-bit machines, the default type *int* is commonly large enough to satisfy what used to require a variable of type **long**. The **long long** type was introduced more recently to handle very large numeric values.

Some computers are better at dealing actually big numbers so the size of the data types will be bigger on these machines. To find out the size of each data type on your computing machine compile and run this piece of code. It uses one new language concept sizeof (). This tells you how many bytes a data type accepts.

# ## DATA TYPES AND STORAGE

To store data inside the computer we need to first identify the type of data elements we need in our program. There are several different types