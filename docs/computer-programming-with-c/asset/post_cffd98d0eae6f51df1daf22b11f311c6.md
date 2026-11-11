
```cpp
cout<<"Enter id name and salary"<<endl;
cin>>id>>name>>salary;
}
void output()
{
cout<<"id="<<id<<" name="<<name<<" salary="<<salary<<endl;
}
};
void main()
{
    /*Create Employee objects*/
    Employee e1,e2,e3;
    e1.input();
    e2.input();
    e3.input();
    /*Create Organization.txt in write mode*/
    ofstream fout("Organization.txt");
    /*Write three Employee objects into the file Organization.txt
    using fout*/
    fout.write((char*)&e1,sizeof(e1));
    fout.write((char*)&e2,sizeof(e2));
    fout.write((char*)&e3,sizeof(e3));
    fout.close();
        /*Read objects back from file and print on the computer
        screen. We have intentionally created a object temp,
        which will store one employee read from the file in any
        particular iteration of the loop*/
        Employee temp;
        /*Open Organization.txt in read mode*/
        ifstream fin("Organization.txt");
        /*Iterate the file Organization.txt*/
        while(!fin.eof())
        {
        /*Read an Employee object from file and store it in temp*/
        fin.read((char*)&temp,sizeof(temp));
        /*Print the object read from file on computer screen*/
        cout<<"Object read"<<endl;
        temp.output();
        }
fin.close();
}
```

## Output

```text
Enter id name and salary
10 John 5000
Enter id name and salary
20 Jack 3000
Enter id name and salary
30 Jill 8000
Object read
id=10 name=John salary=5000
Object read
id=20 name=Jack salary=3000
Object read
id=30 name=Jill salary=8000
```

### Notes

We have to use read() and write() functions to read/write object to the file. This is because every object must be transferred to/from the file in binary format.

### Scratch Pad

After execution of the program it is recommended that you open Organization.txt and see its data contents. It will all appear as junk to you because this data is written in binary format; however the data has meaning to C++ so please do not attempt to change this file.

### Solved Example 15.7

After writing Employee objects in the file named as Organization.txt, change the program given in Solved Example 15.6 to accept the id of the employee as input from the user and to delete the corresponding Employee object with the matching id from the file.

```cpp
#include<iostream.h>
#include<fstream.h>
#include<string.h>
class Employee
{
private:
    int id;
    char name[100];
    int salary;
public:
    void input()
    {
        cout<<"Enter id name and salary"<<endl;
        cin>>id>>name>>salary;
}
void output()
{
cout<<"id="<<id<<" name="<<name<<" salary="<<salary<<endl;
}
/*New method added to get the id of the employee object*/
int getId()
{
        return id;
}
};
void main()
{
        /*Create Employee objects*/
        Employee e1,e2,e3;
        e1.input();
        e2.input();
        e3.input();
        /*Create Organization.txt in write mode*/
        ofstream fout("Organization.txt");
        /*Write Employee objects into the file Organization.txt
        using fout*/
        fout.write((char*) &e1,sizeof(e1));
        fout.write((char*) &e2,sizeof(e2));
        fout.write((char*) &e3,sizeof(e3));
        fout.close();
        /*Take the id of employee to be deleted from the file as
        input*/
        int delId;
        cout<<"Enter the ID of the employee to be deleted from the
        file"<<endl;
        cin>>delId;
        /*Create a temp file to store all records except the record
        which is to be deleted*/
        fout.open("Rec_temp.txt",ios::out);
        /*Read objects back from file and print on the computer
        screen. We have intentionally created an object temp, which
        will store one employee read from the file in any particular
        iteration of the loop*/
        Employee temp;
        /*Open Organization.txt in read mode*/
        ifstream fin("Organization.txt");
        /*Iterate the file Organization.txt*/
        int flag=0;
while(!fin.eof())
{
        /*Read an employee object from file and store it in temp*/
        fin.read((char*)&temp,sizeof(temp));
        /*Check if this is the employee to be deleted*/
        if(temp.getId()==delId)
        {
                flag=1;
                cout<<"Employee Deleted"<<endl;
        }
        else
        {
                /*Write the record in temp file*/
                fout.write((char*)&temp,sizeof(temp));
        }
}
if(flag==0)
{
        cout<<"Employee with id="<<delId<<"does not exist."<<endl;
}
fin.close();
fout.close();
/*Copy all records from Rec_temp.txt to a new file created
as Organization.txt. Note that, we will create a new file
Organization.txt from scratch which will overwrite the
existing file. Hence the old Organization.txt is deleted and
replaced with new empty Organization.txt*/
fout.open("Organization.txt",ios::out);
/*Open Rec_temp.txt in read mode*/
fin.open("Rec_temp.txt",ios::in);
char value;
        while(!fin.eof())
        {
                /*Read next object from temp file Rec_temp.txt */
                fin.read((char*)&temp,sizeof(temp));
                /*Write the object into temp file - Organization.txt*/
                fout.write((char*)&temp,sizeof(temp));
        }
fin.close();
fout.close();
/*Read back records from Organization.txt to ensure that the
Employee object is not present in the file*/
cout<<"Data in file after deletion is as below"<<endl;
fin.open("Organization.txt",ios::in);
while(!fin.eof())
{
    /*Read an employee object from file and store it in temp*/
    fin.read((char*)&temp,sizeof(temp));
    temp.output();
}
}
```

```text
Output
Enter id name and salary
10 John 2000
Enter id name and salary
20 Jack 4000
Enter id name and salary
30 Jill 5000
Enter the ID of the employee to be deleted from the file
20
Employee Deleted
Data in file after deletion is as below
id=10 name=John salary=2000
id=30 name=Jill salary=5000
```

## Review Questions

- 1. What is streaming input/output? Explain with example.
- 2. Give a list of streaming classes in C++ for console input/output and file input/output. Explain the purpose of each class in short.
- 3. Differentiate between formatted and unformatted I/O operations.
- 4. Differentiate between ASCII mode and binary mode files. Explain how read/write operations are performed in C++ for each of these files.
- 5. Write a short note on ios flags.
- 6. Explain the different modes in which file can be opened in C++.
- 7. Write a program to accept 100 numbers as input from a file. Perform the addition of all the numbers and store the result of addition back in the same file.

## Chapter 16 | Templates in C++

### 16.1 Overview

Templates in C++ are used to facilitate generic programming by giving the programmer an ability to create generic classes/functions in the program. A component of the program is said to be generic if its functionality remains the same irrespective of data type of the values it operates on. A **generic function** is a function that can work with arguments of any data type, whereas a **generic class** is a class that can work with members of any data type. In this chapter, we will learn creation of generic functions using **function templates** and creation of generic classes using **class templates**.

> **Notes**
>
> The objective of templates is to create generic components in the program, which can work with different data types. This saves programmers effort to define the same component multiple times and replicating same logic for different type of data values.

### 16.2 Function Templates

Function templates in C++ enable the programmer to create generic functions. These functions are adaptable to multiple data types and can execute in the same way immaterial of the data type of the values passed to it.

The functions we have written so far in the previous chapters are strictly bonded to specific types. For example, consider the function add() as shown below:

```cpp
int add(int a, int b)
{
    int c = a+b;
    return c;
}
```

The function takes two arguments of type integer and returns the resultant integer, which gives addition of two numbers. This function works well if integer values are
