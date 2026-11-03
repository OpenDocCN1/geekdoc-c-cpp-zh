
10.12 (Packing Characters into an Integer) The left-shift operator can be used to pack four character values into a four-byte unsigned int variable. Write a program that inputs four characters from the keyboard and passes them to function packCharacters. To pack four characters into an unsigned int variable, assign the first character to the unsigned int variable, shift the unsigned int variable left by 8 bit positions and combine the unsigned variable with the second character using the bitwise inclusive OR operator. Repeat this process for the third and fourth characters. The program should output the characters in their bit format before and after they're packed into the unsigned int to prove that the characters are in fact packed correctly in the unsigned int variable.

10.13 (Unpacking Characters from an Integer) Using the right-shift operator, the bitwise AND operator and a mask, write function unpackCharacters that takes the unsigned int from Exercise 10.12 and unpacks it into four characters. To unpack characters from a four-byte unsigned int, combine the unsigned int with the mask 4278190080 (11111111 00000000 00000000 00000000) and right shift the result 8 bits. Assign the resulting value to a char variable. Then combine the unsigned int with the mask 16711680 (00000000 11111111 00000000 00000000). Assign the result to another char variable. Continue this process with the mask 65280 and 255. The program should print the unsigned int in bits before it's unpacked, then print the characters in bits to confirm that they were unpacked correctly.

10.14 (Reversing the Order of an Integer's Bits) Write a program that reverses the order of the bits in an unsigned int value. The program should input the value from the user and call function reverseBits to print the bits in reverse order. Print the value in bits both before and after the bits are reversed to confirm that the bits are reversed properly.

10.15 (Portable displayBits Function) Modify function displayBits of Fig. 10.7 so it's portable between systems using 2-byte integers and systems using 4-byte integers. [Hint: Use the sizeof operator to determine the size of an integer on a particular machine.]

10.16 (What's the Value of X) The following program uses function multiple to determine if the integer entered from the keyboard is a multiple of some integer X. Examine the function multiple, then determine X's value.

```c
// ex10_16.c
// This program determines whether a value is a multiple of X.
#include <stdio.h>

int multiple(int num); // prototype

int main(void)
{
   int y; // y will hold an integer entered by the user

   puts("Enter an integer between 1 and 32000: ");
   scanf("%d", &y);

   // if y is a multiple of X
   if (multiple(y)) {
      printf("%d is a multiple of X\n", y);
   } else {
      printf("%d is not a multiple of X\n", y);
   }
}

// determine whether num is a multiple of X
int multiple(int num)
{
   int i;
   26    int mask = 1; // initialize mask
   27    int mult = 1; // initialize mult
   28
   29    for (int i = 1; i <= 10; ++i, mask <<= 1) {
   30        if ((num & mask) != 0) {
   31            mult = 0;
   32            break;
   33        }
   34    }
   35
   36    return mult;
   37 }
   38 }
```

10.17 What does the following program do?

```c
1    // ex10_17.c
2 #include <stdio.h>
3
4 int mystery(unsigned int bits); // prototype
5
6 int main(void)
7 {
8     unsigned int x; // x will hold an integer entered by the user
9
10    puts("Enter an integer: ");
11    scanf("%u", &x);
12
13    printf("The result is %d\n", mystery(x));
14 }
15
16 // What does this function do?
17 int mystery(unsigned int bits)
18 {
19    unsigned int mask = 1 << 31; // initialize mask
20    unsigned int total = 0; // initialize total
21
22    for (unsigned int i = 1; i <= 32; ++i, bits <<= 1) {
23
24        if ((bits & mask) == mask)
25            ++total;
26    }
27
28    return !(total % 2) ? 1 : 0;
29
30 }
```

10.18 *(Fisher-Yates Shuffling Algorithm)* Research the Fisher-Yates shuffling algorithm online, then use it to reimplement the shuffle method in Fig. 10.3.

## Making a Difference

10.19 *(Computation of Health Records)* A health care issue that has been in the news lately is the computerization of health records. This possibility is being approached cautiously because of sensitive privacy and security concerns, among others. Computerizing health records could make it easier for patients to share their health profiles and histories among their various health care professionals. This could improve the quality of health care, help avoid drug conflicts and erroneous drug prescriptions, reduce costs and in emergencies could save lives. In this exercise, you'll design a "starter" HealthProfile structure for a person. The structure's members should include the person's first name, last name, gender, date of birth (consisting of separate attributes for the month, day and year of birth), height (in inches) and weight (in pounds). Your program should have a function that receives this data and uses it to set the members of a HealthProfile variable. The program also should include functions that calculate and return the user's age in years, maximum heart rate (see Exercise 3.47), and body mass index (BMI; see Exercise 2.32). The program should prompt for the person's information, create a HealthProfile variable for that person and display the information from that variable—including the person's first name, last name, gender, date of birth, height and weight—then calculate and display the person's age in years, BMI, maximum heart rate and target-heart-rate range. It should also display the "BMI values" chart from Exercise 2.32.

## C File Processing

### Objectives

In this chapter, you'll:

- Understand the concepts of files and streams.
- Create and read data using sequential-access file processing.
- Create, read and update data using random-access file processing.
- Develop a substantial transaction-processing program.
- Study Secure C programming in the context of file processing.

## Communication Channels

Streams provide communication channels between files and programs. For example, the standard input stream enables a program to read data from the keyboard, and the standard output stream enables a program to print data on the screen.

## FILE Structure

Opening a file returns a pointer to a FILE structure (defined in `<stdio.h>`) that contains information used to process the file. In some operating systems, this structure includes a file descriptor, i.e., an integer index into an operating-system array called the open file table. Each array element contains a file control block (FCB)—information that the operating system uses to administer a particular file. The standard input, standard output and standard error are manipulated using `stdin`, `stdout` and `stderr`.

## File-Processing Function fgetc

The standard library provides many functions for reading data from files and for writing data to files. Function `fgetc`, like `getchar`, reads one character from a file. Function `fgetc` receives as an argument a FILE pointer for the file from which a character will be read. The call `fgetc(stdin)` reads one character from `stdin`—the standard input. This call is equivalent to the call `getchar()`.

## File-Processing Function fputc

Function `fputc`, like `putchar`, writes one character to a file. Function `fputc` receives as arguments a character to be written and a pointer for the file to which the character will be written. The function call `fputc('a', stdout)` writes the character 'a' to `stdout`—the standard output. This call is equivalent to `putchar('a')`.

## Other File-Processing Functions

Several other functions used to read data from standard input and write data to standard output have similarly named file-processing functions. The `fgets` and `fputs` functions, for example, can be used to read a line from a file and write a line to a file, respectively. In the next several sections, we introduce the file-processing equivalents of functions `scanf` and `printf`—`fscanf` and `fprintf`. Later in the chapter we discuss functions `fread` and `fwrite`.

## 11.3 Creating a Sequential-Access File

C imposes no structure on a file. Thus, notions such as a record of a file are not part of the C language. The following example shows how you can impose your own record structure on a file.

Figure 11.2 creates a simple sequential-access file that might be used in an accounts receivable system to keep track of the amounts owed by a company's credit clients. For each client, the program obtains an account number, the client's name and the client's balance (i.e., the amount the client owes the company for goods and services received in the past). The data obtained for each client constitutes a "record" for that client. The account
