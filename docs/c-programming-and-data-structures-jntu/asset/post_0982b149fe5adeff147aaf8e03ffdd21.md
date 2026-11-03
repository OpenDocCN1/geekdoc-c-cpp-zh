
The various steps involved in program development are as follows

- 1. Editing phase
- 2. Compilation phase
- 3. Linking phase
- 4. Execution phase

## Editing Phase

In the editing phase, a C program is entered into a file through a text editor. Unix operating system provides a text editor which can be accessed through the Command 'vi'. Modern, compiler vendors provide Integrated Development Environment IDEs. The file is saved on the disk with an extension of 'C'. Corrections in the program at later stages are done through these editors. Once the program has been written, it requires to be translated into machine language.

## Compilation Phase

This phase is carried out by a program called as compiler. Compiler translates the source code into the object code. The compilation phase cannot be proceeded successfully until and unless the source code is error-free. The compiler generates messages if it encounters syntactic errors in the source code. The error-free source code is translated into object code and stored in a separate file with an extension '.obj'.

## Linking Phase

In this phase, the linker links all the files and functions with the object code under execution. For example, if a user uses a 'printf' function in his/ her program, the linker links the user program's object code with the object code of the printf function. Now the object code is ready for next phase.

## Execution Phase

In this phase, the executable object code is loaded into the memory and the program execution begins. We may encounter errors during the execution phase even though compilation phase is successful. The errors may be run-time errors and logical errors.

## 2. Write a program to find the sum of a given series by using function with argument and return value e= 2+3/1!-6/2!+9/3!-12/4!.....!
Ans:

### Program:

```
#include<stdio.h>
#include<math.h>
long fact(int);
```

```
```c
void main()
{
	int x,i,n;
	float s=0,c;
	clrscr();
	printf("\n enter the value of x");
	scanf("%d",&x);
	/*perform the looping operation*/
	for(i=0,n=0;i<n;i=i+2,n++)
	s=s+(pow(-1,n)*pow(x,i)/fact(i));
	printf("\n the result is %f",s);
	getch();
}
/* calling sub program*/
long fact(int x)
{
	long int y=1;
	while(x!=0)
	{
		y=y*x;
		x--;
	}
	return y;
}
```
```

## 3. Write a program and explain the working of malloc() and calloc() functions.

Ans. Memory space is required by the variable in a program to calculate, and assign during execution. The process of allocating memory at runtime is known as dynamic memory allocation. There are some memory management functions in C that can be used for allocating and freeing memory during program execution.

- Some memory allocation functions are

- Malloc() Allocates required size of bytes and returns a pointer to the first byte of allocated space.

- Calloc() Allocates space for an array of elements, initializes them to zero and then returns a pointer to the memory.

- Free() Free previously allocated space.

- Realloc() Modifies the size of previously allocated space.

Memory allocation using malloc() function:

Block of memory may be allocated using malloc() function. Malloc() function reserves a block of memory of specified size and returns a pointer of typed void.

### Syntax:-

```
Ptr=(cast-type*)malloc(byte size);
```

Ptr- pointer of cast type.

Malloc returns a pointer (of cast type) to an area of memory with the size of given bytes.

Example: - y=(int*)malloc(100*sizeof(int));

Malloc allocates a block of contiguous bytes. The allocation can fail if the space in the heap is not sufficient. If it fails, it returns null.

Example program that uses a table of integers whose size will be specified interactively at run time.

```
#include<stdio.h>
#define null 0
Main()
{
int *p,*table;
int size;
printf("enter size of table");
scanf("%d", &size);
printf("\n");
if (table=(int*)malloc(size*sizeof(int))==null)
{
printf("no space available");
exit(1);
}
printf("address of first byte is %u",table);
printf("input table values");
for(p=table;p<table+size;p++)
scanf("%d",&p);
for(p=table+size-1;p>=table;p--)
Printf("%d is stored address %u",*p,p);
}
```

## Memory allocation using calloc() function:-

Calloc() is another memory allocation function that is normally used for requesting memory space at run time for storing derived data types such as arrays and structures. Malloc allocates a single block of storage, each of them, being of the same size, and then sets all bytes to zero.

The general form of calloc() is

```
Ptr=(cast_type*)calloc(n, elem_size);
```

The above statement allocates contiguous space for n blocks, each of size elem_size bytes. All bytes are initialized to zero and a pointer to first byte of the allocated region is returned. If there is not enough space a null pointer is returned. Calloc() allocates blocks of memory.

Calloc takes two arguments which are number of elements to allocate memory and size in bytes of a single variable.

Calloc initializes the allocated memory to zero.

```
#include<stdio.h>
#include<stdio.h>
#define null 0
Main()
{
    Char *buffer;
    If(buffer=(char*)malloc(10)==null)
    {
    printf("malloc failed");
    exit(1);
    }
    Printf("buffer of size %d created \n",msize(buffer));
    Strcpy(buffer,"hyderabad");
    Printf("buffer contains%s",buffer);
    If (buffer=(char*) realloc(buffer,15)!=null)
    {
        Printf("reallocation failed");
        Exit(1);
    }
    Printf("buffer size modified");
    Printf("buffer still contains %s \n",buffer);
    Strcpy(buffer, "secunderabad");
    Printf("\n buffer now contains %s \n",buffer);
    Free(buffer);
}
```

## 4. Define structure and write the general format for declaring and accessing members.

Ans. Structure can store data items in consecutive memory locations. The advantage of structures is that the data items may be of different data types.

Declaring structures:

```
Struct student
{
    Char name [20];
    Int sno,    (1)
}
```

## C.68 Solved Question Papers

```
```c
{
Struct st_record
{
Int weight;
Float height;
};
Static struct st_record st1=(60,180,75);
Static struct st_record st2={53,170,60};
-----------
}
```
```

(OR)

```
```c
Struct st_record
{
Int weight;
Float height;
} st1={60,180,75};
Main (0)
{
Static struct st_record st2={53,170,60};
-----------
}
```
```

Structure members can be accessed by writing variable name.member Dot (.) operator links structure variable to the data member. It is the highest precedence operator and associatively is left to right.

One way is to assign values at the time of declaring structure variables.
Struct person p1={"ravi", "21", "male", "student"};

Another way is to assign values to each member separately as shown below.

```
```c
Strcpy(p1.name, "ravi");
p1.age=21;
Strcpy(p1.gender, "male");
Strcpy(p1.occupation, "student");
```
```

Here is an example demonstrating the structure with initialized values.

```
```c
/* structure with initialized values */
#include<stdio.h>
#include<conio.h>
Void main ( )
{
```
```

## Solved Question Papers C.69

```
```
Struct organization {
	char name[20] ;
	Char designation[20] ;
	Int sal ;
};
```
```

```
```
Struct organization emp1={"ramu", "secretary", "8000"};
Struct organization emp2={"raju", "manager", "18000"};
Printf("details of employee one =%c%c%c%d",emp1.name ,emp1.designation ,emp1.sal);
Printf("details of employee one =%c%c%c%d",emp2.name ,emp2.designation ,emp2.sal);
```
```

A file is a collection of records. Each record provides an information to the user. These files are arranged on the disk and can be accessed through file handling information provided by the standard 'C' library.

The files consist of large amount of data which can be read or modified depending upon the requirement. The basic operations that are performed on files are

- 1. Opening a file
- 2. Reading or writing a file
- 3. Closing a file

These operations are carried out with the help of a structure FILE (stdio.h) and a file pointer.

There are two types of files. They are
1. Sequential file
2. Random access file

In a sequential file system, records are stored in a serial order and retrieved in the same order. If a read operation is to be performed on the last record, then all the records before the last record need to be read because of which a lot of time is wasted.

In sequential access of a file, data is read from or written sequentially i.e., from beginning of the file to end of the file in order. It is achieved using functions fprintf(), fscanf(), getc(), putc() etc. In random access of a file, a particular part of a file can be accessed irrespective of other parts.

Random access of files is achieved with the help of functions fseek(), fseek() and rewind () which are available in I/O library. The functionality of each of these functions are given below.
