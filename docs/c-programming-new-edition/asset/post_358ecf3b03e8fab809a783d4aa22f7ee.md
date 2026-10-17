
The keywords must be written in lowercase only. The message to be displayed through the print statements cannot be given without the quotations. Initially, you were given brief details on the evolution of C.

Following this was a brief overview about the nature of programming languages and in specific the structure of a C program. Later the process of compiling a C program was dealt with after which a short discussion about compilers and interpreters followed.

Pseudocodes were mentioned and then a sample C program was disintegrated & explained and subsequently you learnt about the tabular format, the character set, keywords & the hierarchy of operations was dealt with. Consequently, at the end of the session you were apprised of the rules of the game.

## Going Over It Again:

Fill in the blanks:

- 1. All executable statements in a C program must be terminated with a ____________.
- 2. C programs are written in ______________ case.
- 3. Keywords in C are written in ____________ case.
- 4. C was developed by ____________________.
- 5. The formatted output function in C is ________________.

## True or False:

- 1. Keywords in C are a set of predefined words.
- 2. C was evolved from BPCL.
- 3. A C program can be written without a main() function.
- 4. There are 35 keywords in C.
- 5. The comment statement has no effect on the program while execution.

## One Line Answers:

- 1. What are the three broad sections of a typical C program?
- 2. What is meant by a pseudocode?
- 3. What is the difference between an compiler and an interpreter?

In the previous section or chapter, you get acquainted with the fundamentals of C. In this session you will deal with the core issues that constitute the heart of C. It is these issues on which the mighty fort of C holds firm.

## 2.1. BASIC DATA TYPES

The language of C, magnanimous as it is, supports several different types of data, each of which is represented in a varied manner within the memory. The data in the memory can be of integer type or of character type or of integers with decimal points. Whenever an integer or a character is used in a program, the computer should be able to identify where to store it in the memory. Just imagine the commotion caused when a character is stored in place of an integer. To avoid this, only the basic data types along with their memory requirements have been included The basic data types are depicted in a tabular format to get a better understanding of the basics of C programming.

### 2.1.1. Data Description Memory Range

Int whole numbers 2 bytes −32768 to %d, %i +32768 Char Characters 1 byte 0 to 255%c, %s Float Numbers 4 bytes 1.0E-37 to %f with decimals 1.0E+37 Double Numbers 8 bytes 2.2E-308 to with large decimals 2.2E+308. Now that the data types are represented in a very comprehensible pattern you can scan each data type individually. int This particular data type deals in storing only whole integer numbers and they are incapable of dealing with fractions or numbers with decimals (Figure 2.1).

| Type | Bytes | Values |
|---|---:|---|
| int | 2 or 4 | -32, 768 to 32, 767 |
| unsigned int | 2 or 4 | 0 to 65, 535 |
| signed int | 2 or 4 | -32, 767 to 32, 767 |
| short int | 2 | -32, 767 to 32,767 |
| unsigned short int | 2 | 0 to 65, 535 |
| signed short int | 2 | -32, 767 to 32, 767 |
| long int | 4 | -2,147,483,647 to 2,147,483,647 |
| signed long int | 4 | -2,147,483,647 to 2,147,483,647 |
| unsigned long int | 4 | 0 to 4, 294,967,294 |

**Figure 2.1.** Data types in C programming.

The numbers which they can deal with range from −32,768 to +32,768. An int requires 2 bytes of memory by most computers. char The char data type holds individual characters or alphabets and they require only 1 byte of memory. Most compilers permit a range of 0 to 255 regarding the char data type. float A float data type is involved in restoring floating point numbers or to put it simply, it is used to store numbers with decimal point (e.g., 67.25).

The float desires 4 bytes for storage and has a fractional precision of 6 digits. double A double data type is also used for the restoration of floating point numbers. The difference lies in the precision and storage space. Double offers a greater precision, of about 15 digits and compilers require 8 bytes to store a double. The ranges within which the float can be represented are 2.2E-308 and 2.2E+308 respectively.

## 2.2. QUALIFIERS USED WITH BASIC DATA TYPES

You are aware of what the basic data types are. To simplify, qualifiers can be thought of as steroids to the basic data types, that is to say they are power boosters. The efficiency of the data types can be augmented by the use of these qualifiers, which expand the horizon of the basic data types, making it more flexible and adaptable to get into various situations with preciseness and accuracy.

The qualifiers tagged to the data types are LONG, SHORT, SIGNED, and UNSIGNED. To make any data type a qualifier, the name of the qualifier has to be tagged before the data type. long As the name suggests, the qualifier long extends the range of the data type to which it is prefixed. It can be applied to only the int and double data types and it expands the spectrum of range from a maximum of 2,147,483,647 to −2,147,483,647. A long int requires memory that is more than an ordinary int and therefore takes 4 bytes for storage.

To make an integer a long qualifier just add the word long before it. Short This qualifier is most interesting, because if an ordinary int has the same memory value as that of long, i.e., 4 bytes a short will have 2 bytes, but if an int has memory of 2 bytes a short will have the same memory, i.e., 2 bytes. Signed by using a signed data qualifier that data type can accommodate both positive and negative numbers. When a variable is signed it has the same positive and negative ranges as a regular int.

By default, an int is a signed data type. Unsigned The qualifier unsigned is tagged mostly to int and it also has the same memory requirement as that

of the ordinary int, i.e., 2 bytes. So, you may ask where does the difference lie between both of them. The difference is evident in the range it offers. The range this particular qualifier boasts of is twice that of the ordinary int. To put it in numbers unsigned int has a range varying from 0 to 65,535.

Another doubt that may now disturb you is the difference between unsigned and long. One important fact to be restored in the subconscious level of the mind is that an unsigned int cannot store negative numbers unlike long. The unsigned int can be applied to other int qualifiers like unsigned short int and unsigned long int.

## 2.3. THE VARIABLES IN C

Consider you have some money and you want to store it in a safe place. The best place you can think of is the bank and you save it in your account, which has an id number. Thus, whenever you want to retrieve the money you can do so by flashing the id so that the bank authorities can recognize your money is in that particular account.

In a similar way you have a number and you have to store it in some safe place so that it can be retrieved and used whenever required. Here you store it in the memory (the bank) OK, so you have stored your number in the memory. But where? Why such a query arises is because the memory is so expansive and that a tiny little number can be stored anywhere. To identify where it has been stored you can name the location (the account) and that name is called variable name (account id). Whenever the need arises for the utilization of the number it can be recalled from the memory using the variable name which helps the computer to identify in which location the number is stored and extracts the number and uses it for computation. These locations can hold either an integer or a real constant or a character and they cannot hold more than one at a time. The location which is allotted for an integer can hold only an integer and nothing else. It is the same case for the other types.

Given below are valid examples:

- - **Example 2.1:** The first character in the variable name must always be an alphabet. In the above example you can see that all of them start with the alphabet c. Don’t include any commas or blank spaces or special symbols within a variable name. Only underscore is allowed. (Not fair is it?) Now that you have created a variable name, how does the computer understand whether the variable will contain an integer or a character or a floating point.
