Every variable is associated with a particular data type. A data type of a variable determines the type of value that can be stored inside the variable. The list of basic data types which are supported by C/C++ is given below:

| Data type | Description | Size in bytes | Range of values |
|---|---|---:|---|
| `int` | A variable of type int can store any integer type of constant which falls under the range of −32,768 to +32,767 | 2 bytes | −32,768 to +32,767 |
| `float` | A variable of type float can store any number with a decimal point which falls under the range of −3.4e−38 to +3.4e+38 | 4 bytes | −3.4e−38 to +3.4e+38 |
| `char` | The data type char is used to store character constant which is single symbol enclosed in the single quotes | 1 byte | −128 to +127 |
| `double` | A variable of type double can store any number with a decimal point which falls under the range of −1.7e−308 to +1.7e+308. This data type has higher precision when compared to float. Hence a double type variable requires 8 bytes in the memory whereas the float type of variable just requires 4 bytes in the computer memory | 8 bytes | −1.7e−308 to +1.7e+308 |
| `short int` | A variable of type short int can store any integer type of constant which falls under the range of −128 to +127. The keywords short int define a smaller version of the int type in C++. Hence, the short int type of variables just requires 1 byte in the computer memory, whereas the int variable actually requires 2 bytes in the computer memory | 1 byte | −128 to +127 |
| `long` | A variable of type long can store any integer type of constant which falls under the range of −2147483648 to +2147483647. The keyword long represents the larger version of the int type in C++. Hence, the long type of variables requires 4 bytes in the computer memory whereas the int variable just requires 2 bytes in the computer memory | 4 bytes | −2147483648 to +2147483647 |

¹ We assume 16 bit compiler throughout this text book where size of an integer is 2 bytes (16 bits). If you get the size of integer as 4 bytes it means you are working on a 32 bit compiler.

# 2.5.1 Evaluating the range of data types

The range of values which can be stored inside a variable of a particular type is dependent on the size of that ‘data type’ in the computer memory. The range of a particular data type can be decided by considering the total number of permutations that can be represented by the bit values assigned to the variable. As an example, let us consider an integer type variable which requires 2 bytes in the computer memory. As each byte is formed using eight bits, we can say that an integer variable requires 16 bits in the computer memory. Therefore, the total number of permutations (X) that can be represented using 16 bits can be calculated as shown below:

Number of permutations (X) = 2¹⁶ = 65,536