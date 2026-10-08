
```c
/** End of function main */

/** Beginning of function getcontact */
void getcontact(struct contact *ptrcontact)
{
char c_temp;
printf("\n Enter name : ");
scanf("%[^\n]",ptrcontact->c_name);
c_temp=getchar();
printf("\n Enter e-mail address : ");
scanf("%[^\n]",ptrcontact->c_email);
printf("\n Enter phone number : ");
scanf("%ld",&ptrcontact->li_phono);
}
/** End of function getcontact **/
```

**Output:**

Enter name: Anya Gangele

Enter e-mail address: anya@gmail.com

Enter phone number: 20110222

The values recently entered by you are as under:

Name: Anya Gangele

E-mail address: anya@gmail.com

Phone number: 20110222

Program 17 contains a function named getcontact. It accepts one parameter. The type of parameter as defined in its prototype is pointer to a structure. The manipulations are done on structure members within a function. The control is returned back to the calling function once the values of the structure members are accepted from the user and stored in the respective data members of a structure. These values are then displayed in the main function. The values input by the user and stored in the structure contact1 are available in the calling function because we passed the address of the structure to function getcontact at the time of function call. The manipulations are done directly on memory locations.

## Summary

In this chapter, we have revised the concept of pointers. The detailed knowledge of pointers is required to work with pointers and used them for efficient programming. We have also seen how chain of pointers can be created. The pointer arithmetic used for address calculations in single-dimensional and two-dimensional arrays are also discussed in detail in this chapter. The usage of pointers with functions is explained with examples. We also discussed how to use pointers along with structure.

## Review Questions

- Q1. What is a pointer?
- Q2. What are the benefits of using pointers in C language?
- Q3. Give the significance of & and * operators.
- Q4. What do you understand by a pointer to a pointer?
- Q5. Usage of pointers makes execution of program faster. Comment on this statement.
- Q6. Explain giving example the arithmetic operations that can be performed on pointer variables.
- Q7. Explain how one-dimensional array can be accessed using pointer notation.
- Q8. Explain how two-dimensional array can be accessed using pointer notation.
- Q9. array[j] and i[array] are equivalent. Justify the statement.
- Q10. Explain the concept of pointers to function.
- Q11. Explain the concept of pointer to structure.
- Q12. Given int i_first=30; int i_second=40; int *p1 = &i_first; and *p2 = &i_second. Find the values of the following:
  - i. (*p1)
  - ii. ++ (*p2)
  - iii. *p1 - (*p2) ++
  - iv. -(*p2) + *p1
- Q13. Write the output of the following programs:
  - i. `int main(void) { int i; float *pf; pf = (float *)&i; *pf = 100.00; printf("%d", i); }`
  - ii. `int main(void) { char *a = "Hello"; char *b = "World"; c1stcr(); printf("%s", strcpy(a,b)); }`
- Q14. Differentiate between the following.
  - i. char *ch and char *ch[10]
  - ii. int (*fun)() and int *fun()
  - iii. int *p and int **p
  - iv. char * ch and int *ptr
  - v. &p and *p, where p is a pointer variable.
- Q15. A function q that accepts a pointer to a character as argument and returns a pointer to an array of integer can be declared as:
  - i. int (*q(char*)) []
  - ii. int *q(char*) []
  - iii. int(*q)(char*) []
  - iv. None of the Above
- Q16. State whether the following statements are TRUE or FALSE:
  - i. Pointers can contain only addresses.
  - ii. Pointer cannot point to structure.
  - iii. Accessing values through pointer variables are faster than accessing it with normal variables.
  - iv. If int y = 45; int p1 = &y; then printf("%d" ,**p1); will give value 45.
  - v. Every C function has an address that can be stored in a pointer to a function.

## Practical Exercises

- Q1. Write a program using pointers to read in a string and check whether the string is palindrome or not.
- Q2. Write a menu-driven program that works as a simple calculator. Use functions to perform operations on two numbers. Note that the function should accept pointers to integers.
- Q3. Write a program to find the largest element within an integer array using pointers.
- Q4. Write a program to arrange the numbers of an array in ascending order using pointers.
- Q5. Write a program to perform matrix multiplication using pointers.
- Q6. Write a program to find out whether a matrix is an identity matrix or not using pointers.
- Q7. Write a program to compare two strings using pointers.
- Q8. Write a program to calculate the length of the string using pointers.
- Q9. Write a program to reverse the string using pointers.
- Q10. Write a program that declares a two-dimensional array. With the help of pointers, find the maximum element of each row and the minimum element of each column.
- Q11. Write a program to merge two sorted arrays so that the resultant array is in sorted order using pointers.
- Q12. Write functions to add, multiply, subtract two numbers, and call the functions from the main program using a function pointer.

# 13 Files in C

## OBJECTIVES

- Describe Concept of File
- Describe Files and Streams
- Describe File Operations
- Opening and Closing a File
- Implement Characters and File
- Implement String and File
- Implement Integer and File
- Implement Function f eof
- Implement General I/O in Text Files
- Implement I/O in Binary Files
- Implement Random File Access

In all the previous chapters, we have used input from the keyboard and displayed the output on the monitor. C language provides inbuilt function to handle input/output (I/O) operations. We have seen the use of the function scanf to accept input, the function getchar to read a single character at a time from the keyboard, the function printf for formatted output, the function putchar to output a single character on the monitor, the function gets to read a string from the keyboard, and the function puts to output a string on display terminal. The keyboard and monitor act as standard input and standard output devices.

The aforementioned library functions serve the purpose of the programmers as long as small amount of data is to be processed and temporary input and output are required. However, real-life problems work on large volume of data stored on permanent storage. Voluminous data can be stored in a file and the contents of the file are retained even when the computer is switched off. In this chapter, we will discuss about the concept of files and the two different types of files, namely, text files and binary files. We will also discuss the use of different library functions to perform various operations on files.

## 13.1 Concept of File

A file is a collection of related data. For example, we have created structure in Chapter 11 to store contact details. However, we have observed that the data input by the user are stored in the form of variable values, which are stored in the memory. To retain the contents, these contents are to be transferred to a permanent storage. The primary purpose of a file is to store data in a nonvolatile storage device. The contents of primary memory get lost when the computer is turned off. Files are stored in secondary storage devices. Magnetic disk, commonly referred as hard disk, is the most common secondary storage device. Thus, contact details discussed in Chapter 11 can also be stored in a file. The data in a file can be accessed later whenever required. There are two fundamental types of file, namely, text and binary files. The next section gives an idea about text files.

### Text File

A text file is meant to store textual information such as alphabets, digits, and special symbols in a computer. In real sense, the American Standard Code for Information Interchange (ASCII) codes of these characters are stored in text files. Text files are readable to the users. For example, a C program that we have written in this book can be opened in an editor and read by the user. This suggests that a C program file is a text file. Figure 1 shows examples of text files opened using Notepad editor:

![](img/5d422ba7108ffdf64376be51eaf0c459_291_0.png)

It can be observed in Figure 1 that all the contents of the file, including numbers, are visible to us. The file shown in Figure 1 is an example of fixed-width record. Observe that the contents in all the three columns visible in the figure 1 start at a fixed position and also ends at a fixed position within the file. Figure 2 shows an example of another text file:

![](img/5d422ba7108ffdf64376be51eaf0c459_291_1.png)

In Figure 2, the start point and the end point of the contents cannot be demarked easily. This is a free-format text file. The next section discusses the concept of binary file.
