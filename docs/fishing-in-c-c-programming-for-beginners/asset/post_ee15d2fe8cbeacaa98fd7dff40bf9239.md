
## Copying one structure to another

### Method1: Copying each and every element

This method is used when size or elements of the two structures are different. In this method we copy each and every element from one structure to other.

Consider the following program:

```cpp
#include<iostream>
using namespace std;
struct student
{
 char name[50];
 char section;
 int roll;
};
int main()
{
 struct student s1;
 cout << "Enter the name of student\n";
 gets(s1.name);
 cout << "Enter the section of student\n";
 cin>>s1.section;
 cout << "Enter the roll number of the student\n";
 cin>>s1.roll;

 struct student s2;
 s2.name=s1.name; //Here name is being copied
 s2.roll=s1.roll;//Here roll is being copied
 s2.section=s1.section;//Here section is being copied

 cout<<("\nThe name of student is: ");
 puts(s2.name);
 cout<<("\nThe section of the student is: "<<s2.section);
 cout<<("\nRoll number of the student is: "<<s2.roll);

 return 0;
}
```

### Output

Enter the name of student
Aman Kumar Jha
Enter the section of the student
D
Enter the roll number of the student
12

The name of student is Aman Kumar Jha
The section of the student is: D
Roll number of the student is: 12

### Method2: Copying the structure itself

Compiler also gives us the feature to copy the structure itself instead of copying each and every element. Suppose there is a structure s1 and another s2. Then by just writing s2=s1; all the corresponding elements will be copied. E.g. Consider the following program:

```cpp
#include<iostream>
using namespace std;
struct student
{
 char name[50];
 char section;
 int roll;
};

int main()
{
    struct student s1;
    cout << "Enter the name of student\n";
    gets(s1.name);
    cout << "Enter the section of student\n";
    cin>>s1.section;
    cout << "Enter the roll number of the student\n";
    cin>>s1.roll;

    struct student s2;
    s2=s1;//Here entire structure is copied
    cout<<("\nThe name of student is : ");
    puts(s2.name);
    cout<<("\nThe section of the student is: "<<s2.section);
    cout<<("\nRoll number of the student is: "<<s2.roll);

    return 0;
}
```

This program will give the same output as the previous one.

## Passing structure elements to a function

Structure elements can be passed as arguments to the function like ordinary variables. Following program illustrates this method:

```cpp
#include<iostream>
void display(char* n, char c, int i);
using namespace std;
struct student
{
    char name[50];
    char section;
    int roll;
};
int main()
{
    struct student s1;
    cout << "Enter the name of student\n";
    gets(s1.name);
    cout << "Enter the section of student\n";
    cin>>s1.section;
    cout << "Enter the roll number of the student\n";
    cin>>s1.roll;
    display(s1.name,s1.section,s1.roll);
    return 0;
}
void display(char* n, char c, int i)
{
    cout<<("\nThe name of student is: ");
    puts(n);
    cout<<("\nThe section of the student is: "<<c);
    cout<<("\nRoll number of the student is: "<<i);
}
```

## Passing entire structure to the function

Entire structure can also be passed to the function. Following program illustrates this.

```cpp
#include<iostream>
using namespace std;
struct student
{
    char name[50];
    char section;
    int roll;
};
void display(struct student s2);
int main()
{
    struct student s1;
    cout << "Enter the name of student\n";
    gets(s1.name);
    cout << "Enter the section of student\n";
    cin>>s1.section;
    cout << "Enter the roll number of the student\n";
    cin>>s1.roll;
    display(s1);
    return 0;
}

void display(struct student s2)
{
    cout<<("\nThe name of student is: ");
    puts(s2.name);
    cout<<("\nThe section of the student is: "<<s2.section);
    cout<<("\nRoll number of the student is: "<<s2.roll);
}
```

## Structure as return type

Structure can be used as a return type also. Following program illustrates this fact:

```cpp
#include<iostream>
using namespace std;
struct student
{
    char name[50];
    char section;
    int roll;
};
struct student input();
int main()
{
    struct student s2=input();
    cout<<("\nThe name of student is: ");
    puts(s2.name);
    cout<<"\nThe section of the student is: "<<s2.section;
    cout<<"\nRoll number of the student is: "<<s2.roll;
    return 0;
}

struct student input()
{
    struct student s1;
    cout << "Enter the name of student\n";
    gets(s1.name);
    cout << "Enter the section of student\n";
    cin>>s1.section;
    cout << "Enter the roll number of the student\n";
    cin>>s1.roll;
    return s1;
}
```

Here, input() is a function which returns an entire structure.

## Structure as a pointer

Structure can have pointers. With pointer, dot operator is not used rather arrow operator(->) is used. Consider the following program

```cpp
#include<iostream>
using namespace std;
struct student
{
char name[50];
char section;
int roll;
};
int main()
{
    struct student s1;

    cout << "Enter the name of student\n";
    gets(s1.name);

    cout << "Enter the section of student\n";
    cin>>s1.section;
    cout << "Enter the roll number of the student\n";
    cin>>s1.roll;
    struct student* s2=&s1;

    cout<<("\nThe name of student is: ");
    puts(s2->name);
    cout<<("\nThe section of the student is: "<<s2->section);
    cout<<("\nRoll number of the student is: "<<s2->roll);
    return 0;
}
```

## File operations

### Useful functions

To operate a file, we use various functions. Some of those are

- open() – This function is used to open a file and returns NULL if not successfully opened.
- close() – This function is used to close the file and returns -1 if cannot close and 0 if successfully closed
- get() – This function is used to get a character from file.
- getline()- This function is used to get a string from the file.

### Useful macros

Three macros are frequently used to operate a file:

- fstream – This class is used to declare a file pointer
- NULL – This has various uses, one of them is to check whether the file is opened successfully or not
- EOF – This macro is used to detect end of file

### Modes to open a file

Files can be operated in various modes. Let us see those modes:

- ios::in: - reading from the file If the file is opened successfully it is loaded into memory and sets up a pointer which points to the first character in it. If the file cannot be opened NULL is returned.
- ios::out: -writing to the file If the file is opened successfully it is loaded into memory and a pointer is sets up which points to the place for writing first character to the file. Existing data in the file will be lost. If there does not exist such file, then a new file will be automatically created. If the file cannot be opened NULL is returned.
- ios::app: - Append output to the end of the file (Should be used in combination with ios::out) If the file is opened successfully then it is loaded into memory and sets up a pointer that points to the last character in it. If the file doesn't exist, a new file is created. Returns NULL, if unable to open file. It does not write anything if not used with ios::out
- ios::trunc: - Discard the file's existing contents (Should be used with ios::out) It is used to reduce the file size to zero, so that a new data can be written to the file.
- ios::binary: - Open the file in binary mode
- ios::ate: - If used with ios::app then it writes to the end of file. If not used with ios::app then it first truncates the file and then performs the operations we want. (Should be used with ios::out)

## Writing to a file

Now, we are going to write in a file. For simplicity I am writing into a file named "example.txt". You can write your desired name in place of "example.txt".

Following program illustrates the simple write operation:

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main()
{
    fstream fout;
    fout.open("example.txt",ios::out);
    if(fout==NULL)
    {
        cout<<("Can't open the file");
        return -1;
    }

    char ch='b';
    char *name="I am Aman";
    int num=5;
    fout<<ch<<endl;
    fout<<num<<endl;
    fout<<name;

    fout.close();
    cout<<"Process completed";
    return 0;
}
```

Output to example.txt
b
5
I am Aman

At first we created an object fout of the class fstream. Then, we used dot operator to access open() function defined in the class. You can create any object of your choice instead of fout and use in similar manner.

fout<< works same as cout<<. So, it can be used to write thrice data, character and string to the file, very simply. Here, in the above program, I have written a character, a number and a string to the file. Similarly, we can use fout>> like cin>>

fout.close() - This function closes the file.
