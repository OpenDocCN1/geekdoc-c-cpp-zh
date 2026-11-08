
**Output**

```text
Enter number of students
2
For student 1
Enter name
Sri
Enter marks
98
For student 2
Enter name
Kiran
Enter marks
96
Name Sri    Marks 98
Name Kiran Marks 96
```

## 77. Write a C program to read name and marks of n number of students from user and store them in a file. If the file previously exists, add the information of n students.

```c
#include <stdio.h>
int main()
{
    char name[50];
    int marks, i, num;

    printf("Enter number of students: ");
    scanf("%d", &num);

    FILE *fptr;
    fptr = (fopen("C:\\student.txt", "a"));
    if(fptr == NULL)
    {
        printf("Error!");
        exit(1);
    }

    for(i = 0; i < num; ++i)
    {
        printf("For student%d\nEnter name: ", i+1);
        scanf("%s", name);

        printf("Enter marks: ");
        scanf("%d", &marks);

        fprintf(fptr, "\nName: %s \nMarks=%d \n", name, marks);
    }

    fclose(fptr);
    return 0;
}
```

**Output**

```text
Enter number of students
1
For student 1
Enter name
Shrutikirti
Enter marks
94
Name Sri    Marks 98
Name Kiran  Marks 96
Name Shrutikirti Marks 94
```

## 78. Write a C program to write all the members of an array of structures to a file using fwrite(). Read the array from the file and display on the screen.

```c
#include <stdio.h>
struct student
{
    char name[50];
    int height;
};

int main()
{
    struct student stud1[5], stud2[5];
    FILE *fptr;
    int i;
    fptr = fopen("file.txt", "wb");
    for(i = 0; i < 5; ++i)
    {
        fflush(stdin);
        printf("Enter name: ");
        gets(stud1[i].name);
        printf("Enter height: ");
        scanf("%d", &stud1[i].height);
    }
    fwrite(stud1, sizeof(stud1), 1, fptr);
    fclose(fptr);
    fptr = fopen("file.txt", "rb");
    fread(stud2, sizeof(stud2), 1, fptr);
    for(i = 0; i < 5; ++i)
    {
        printf("Name: %s\nHeight: %d", stud2[i].name, stud2[i].height);
    }
    fclose(fptr);
}
```

**Output**

```text
Enter name
Sri
Enter Height
5.6"
Enter name
Kiran
Enter Height
5.2"
Enter name
Shrutikirti
Enter Height
5.0"
Enter name
Chirag
Enter Height
5.7"
Enter name
Ravi
Enter Height
5.4"
```

## C Programming

### (Multiple Choice Questions)

Answers are marked by bold and underline

1) The C language consist of ________ number of keywords.

- A] **<u>32</u>**
- B] 40
- C] 24
- D] 56

2) Which of the following is a keyword used for a storage class?

- A] Printf
- B] external
- C] **<u>auto</u>**
- D] scanf

3) The prototype of the function in the header file is _________

- A] Stdio.h
- B] stdLib.h
- C] **<u>conio.h</u>**
- D] io.h

4) Preprocessor Directives are used for _________

- A] Macro Expansion
- B] File Inclusion
- C] Conditional Compilation
- D] **<u>All of these</u>**

5) Which operator has the lowest priority?

- A] ++
- B] %
- C] +
- D] **<u>||</u>**

6) The type cast operator is

- A] **<u>(type)</u>**
- B] cast()
- C] //
- D] " "

7) File manipulation functions in C are available in which header file?

- A] streams.h
- B] **<u>stdio.h</u>**
- C] stdlib.h
- D] files.h

8) Which pair of functions below are used for single character I/O?

- A] **<u>getchar() and putchar()</u>**
- B] scanf() and printf()
- C] input() and output()
- D] None of these

9) Which function is used to read character as you type?

- A] getchar()
- B] getch()
- C] getche()
- D] **<u>Both (B) and (C)</u>**

10) What is the output of this program?

```c
void main()
{
    int a=b=c=10;
    a=b=c=50;
    printf("\n %d %d %d",a,b,c);
}
```

- A) 50 50 50
- B) **Compile Time Error**
- C) 10 10 10
- D) Three Garbage Value

11) Which format specifier is used to print the values of double type variable

- A) %lf
- B) **%ld**
- C) %lu
- D) %f

12) What will be the output of the following program?

```c
void main ( )
{
    double x=28;
    int r;
    r = x%5;
    printf ("\n r=%d", r);
}
```

- A) r= 3
- B) Run time Error
- C) **Compile time Error**
- D) None of the Above

13) What the following function call mean?

```c
Strcpy(s1 , s2);
```

- A) copies s1 string into s2
- B) copies s2 string into s1
- C) copies both s1 and s2
- D) **None of these**

14) What will be the output of the following program?

```c
Void main( )
{
    Int x[] = {10,20,30,40,50};
    Printf (" \n %d %d %d %d %d ", x[4], 3[x], x[2], 1[x], x[0]);
}
```

- A) **Error**
- B) 10 20 30 40 50
- C) 50 40 30 20 10
- D) None of these

15) Which of the following is not a keyword of ‘C’?

- A) auto
- B) register
- C) int
- D) **function**

16) What will be the output?

```c
void main ( )
{
    char a[] = "INFO";
    a++;
    printf("\n %s", a);
}
```

- A] **Error**
- B] INFO
- C] NFO
- D] None of these

17) Which of the following operator has right to left associativity?

- A] &&
- B] //
- C] %
- D] **sizeof**

18) What will be the output?

```c
void main ( )
{
    int I;
    I = 0x10 + 010 + 10;
    printf("\nx=%x", i);
}
```

- A] x=34
- B] i=34
- C] I = 22
- D] **Error**

19) Explicit type conversion is known as

- A] conversion
- B] disjunction
- C] separation
- D] **casting**

20) A C variable cannot start with

- A] A number
- B] A special symbol other than underscore
- C] **Both of the above**
- D] An alphabet

21) By default a function returns a value of type

- A] int
- B] char
- C] **void**
- D] None of these

22) C was primarily developed as

- A] **System programming language**
- B] General purpose language
- C] Data processing language
- D] None of the above

23) What is sizeof In ‘C’?

- A] **Operator**
- B] Reserve Word
- C] Both (A) and (B)
- D] Function

24) C programs are converted into machine language with the help of

- A] An Editor
- B] **A compiler**
- C] An operating system
- D] None of these

25) Which is not keyword in ‘C’?

- A] typedef
- B] const
- C] **near**
- D] none of these

26) Which one of the following is not a valid identifier?

- A] _examveda
- B] **examveda**
- C] exam_veda
- D] examveda1

27) C Language developed at ________?

- A] **AT & T's Bell Laboratories of USA in 1972**
- B] AT & T's Bell Laboratories of USA in 1970
- C] Sun Microsystems in 1973
- D] Cambridge University in 1972

28) Which is the only function all C programs must contain?

- A] start( )
- B] system( )
- C] **main( )**
- D] printf( )

29) Which is valid string function?

- A] strpbrk
- B] **strlen**
- C] strxfrm
- D] strcut

30) Which of the following is not a correct variable type?

- A] float
- B] **real**
- C] int
- D] double

31) We can insert pre written code in a C program by using

- A] #read
- B] #get
- C] **#include**
- D] #put

32) The first expression in a for loop is

- A] Step value of loop
- B] **Value of the counter variable**
- C] Any of above
- D] None of above

33) Break statement is used for

- A] Quit a program
- B] **Quit the current iteration**
- C] Both of above
- D] None of above

34) Continue statement used for

- A] To continue to the next line of code
- B] **To stop the current iteration and begin the next iteration from the beginning**
- C] To handle run time error
- D] None of above

35) What is use of \t in C

- A] used to insert a vertical tab
- B] **used to insert a tab**
- C] places cursor at the end of line
- D] places cursor at the start of line

36) What will be output of

```c
#include <stdio.h>
void main()
{
    char test = 'S';
    printf("\n%c", test);
}
```

- A] **S**
- B] Error
- C] Garbage value
- D] None of above

37) Which of the following is used as a string termination character?

- A] 0
- B] **\0**
- C] /0
- D] None of these

38) Due to variable scope in C

- A] **Variables created in a function cannot be used another function**
- B] Variables created in a function can be used in another function
- C] Variables created in a function can only be used in the main function
- D] None of above

39) What will be the output of following program

```c
#include <stdio.h>
main()
{
    int x, y = 10;
    x = y * NULL;
    printf("%d", x);
}
```

- A] error
- B] **0**
- C] 10
- D] Garbage value

40) Difference between calloc() and malloc()

- A] calloc() takes a single argument while malloc() needs two arguments
- B] **malloc() takes a single argument while calloc() needs two arguments**
- C] malloc() initializes the allocated memory to ZERO
- D] calloc() initializes the allocated memory to NULL

41) Which of the following below is/are valid C keywords

- A] integer
- B] **int**
- C] null
- D] none of above
