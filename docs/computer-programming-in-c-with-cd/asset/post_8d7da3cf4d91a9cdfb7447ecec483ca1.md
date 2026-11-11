
```text
Output:

Enter string :kogent
The copied string1 is = kogent
```

In Listing 24, the `strcpy()` standard library function is used to copy the value stored in the `string1` variable to the `string2` variable.

## The strlen() Function

The `strlen()` function is used to find out the length of a string. It takes one string as an argument to count number of characters in the string. An example of using the `strlen()` function is shown in Listing 25. You can find the Func20.cpp file on the CD in the code/chapter3 folder:

### Listing 25: Using the strlen() Function

```cpp
#include <iostream.h>
#include <string.h>
int main()
{
    char string1[20];
    int length=0;
    cout<<"Enter string :";
    cin>>string1;
    length = strlen(string1); //finding length of string1
    cout<<"Length of string1 is = "<<length;
    return 0;
}
```

```text
Output:

Enter string :kogent
Length of string1 is = 6
```

In Listing 25, the strlen() standard library function is used to find out the length of value stored in the string1 variable.

After understanding function, now let’s discuss the scope of variable that can be accessed from within blocks and functions.

## TEST YOUR KNOWLEDGE

Q11. Write a program to check whether a given string is palindrome or not.

Ans.

```cpp
#include<iostream.h>
#include<string.h>
void main()
{
    char str1[20], str2[20];
    int i;
    cout<<"Enter string :";
    cin>>str1;
    strcpy(str2, str1);
    strrev(str1);
    if(strcmp(str1, str2) == 0)
        cout<<str1<<" is a palindrome";
    else
        cout<<str1<<" is not a palindrome";
}
```

```text
Output:

Enter string :madam
madam is a palindrome
```

Q12. Write a program to find length and reverse of a string.

Ans.

```cpp
#include <iostream.h>
int lengthstr(char ch[])
{
    int count = 0;
    while(count!=NULL)
    {
        if(ch[count] == NULL)
            break;
        count++;
    }
    return count;
}
void revstr(char ch[])
{
    int count = lengthstr(ch);
    cout<<"Reverse of string is ";
    for(int i=count;i>=0;i--)
    {
        cout<<ch[i];
    }
}
void main()
{
    char ch[20];
    cout<<"Enter any string "<<endl;
    cin>>ch;
    cout<<"Length of string is "<<lengthstr(ch)<<endl;
    revstr(ch);
}
```

```text
Output:

Enter any string
computer
Length of string is 8
Reverse of string is retupmoc
```

Q13. Write a program to count the occurrence of a character within a string.

Ans.

```cpp
#include <iostream.h>
#include <string.h>
void main()
{
    char str[20], ch;
    int count=0;
    cout<<"Enter any string "<<endl;
    cin>>str;
    cout<<"Enter any character to find in a given string "<<endl;
    cin>>ch;
    int length = strlen(str);
    for (int i=0;i<length;i++)
    {
        if(str[i] == ch)
            count++;
    }
    cout<<"Character '"<<ch<<"' found "<<count<<" times in "<<str<<endl;
}
```

```text
Output:

Enter any string
alphabet
Enter any character to find in a given string
a
Character 'a' found 2 times in alphabet
```

## 3.3 Scope of Variable

The scope of a variable refers to the region of a program, where variable can be accessed or the area where variable exists in a program. It is a part of program where the variable is accessible or alive. For example, consider the following code snippet:

```cpp
void main()
{
    float i;
    . . .
    . . .
    . . .
}
```

In the preceding code snippet, variable i is only accessible in the main() function, it means that variable i cannot be accessed outside the main() function as a variable declared within a function cannot be accessed outside the function. The two types of scope of variables in C++ are:

- Local variable
- Global variable

### Local Variable

A variable, which is declared within a body of function or within a block, is referred to as a local variable. This variable can be accessed within the function or block in which it is declared. A block is a group of statement that starts with an opening curly brace and ends with a closing curly brace. It means that you cannot access local variable outside the function or block in which it is declared. For example, if you declare a variable x in the main() function then it is accessed only within the main() function. An example of using local variables is shown in Listing 26. You can find the Func21.cpp file on the CD in the code/chapter3 folder:

### Listing 26: Using Local Variable

```cpp
#include <iostream.h>
int main()
{
    int localv1;
    {
        int localv2;
        cout<<"Enter the value of localv1 :";
        cin>>localv1;
    }
    cout<<"Enter the value of localv2 :";
    cin>>localv2;
    return 0;
}
```

Listing 26 generates a compile-time error *Undefined symbol 'localv2'* on statement number 11 (cin>>localv2;). This is how a localv2 is declared within a block and the scope of this variable is alive only within that block, as shown in the following code snippet:

```cpp
{
    int localv2;
    cout<<"Enter the value of localv1 :";
    cin>>localv1;
}
```

In the preceding code snippet, the localv2 variable is used outside the block where it is declared and therefore, it leads to compile-time error.

### Global Variable

A variable, which is declared on the top of a program before calling the main() function, is known as global variable. It means that this variable can be accessed within any block or any function of the program. Listing 27 shows how to use a global variable. You can find the Func22.cpp file on the CD in the code/chapter3 folder:

### Listing 27: Using Global Variable

```cpp
#include <iostream.h>
int global_variable; // global variable
int main()
{
    global_variable = 5;
    void function1();
    int function2();
    cout<<"The value of global_variable in main() function is :"
        <<global_variable<<endl;
    {
        global_variable = global_variable + 10;
        cout<<"The value of global_variable in block of main() function is :"
            <<global_variable<<endl;
    }
    function1();
    int x = function2();
    cout<<"Final value of global_variable is :"<<x;
    return 0;
}
void function1()
{
    global_variable = global_variable - 5;
    cout<<"The value of global_variable in function1() is :"
        <<global_variable<<endl;
}
int function2()
{
    global_variable = global_variable + 50;
    cout<<"The value of global_variable in function2() is :"
        <<global_variable<<endl;
    {
        global_variable = global_variable - 20;
        cout<<"The value of global_variable in block of function2() is :\n"<<global_variable<<endl;
    }
    global_variable++;
    return global_variable;
}
```

Output:

```text
The value of global_variable in main() function is :5
The value of global_variable in block of main() function is :15
The value of global_variable in function1() is :10
The value of global_variable in function2() is :60
The value of global_variable in block of function2() is :40
Final value of global_variable is :41
```

In Listing 27, the global_variable variable is declared as global variable, which is used in the main(), function1() and function2() functions.

## TEST YOUR KNOWLEDGE

Q14. Write a program to show the usage of a global variable.

Ans.

```cpp
#include<iostream.h>
int cars_p,cars_np,tax;
void count()
{
    char x;
    do
    {
        cout<<"Enter p if car paid the tax and n if it didn't paid the tax"<<endl;
        cin>>x;
        switch(x)
        {
            case 'p':
                cars_p++;
                break;
            case 'n':
                cars_np++;
                break;
        }
        cout<<"\nAre there more cars [y/n]"<<endl;
        cin>>x;
    }while(x=='y' || x=='Y');
}
void cal()
{
    tax=5*cars_p;
}
void display()
{
    cout<<"\n Number of cars who paid tax"<<cars_p;
    cout<<"\n Tax collected "<<tax;
    cout<<"\n Number of cars who didn't paid tax "<<cars_np;
}
void main()
{
    count();
    cal();
    display();
}
```

```text
Output:

Enter p if car paid the tax and n if it didn't paid the tax
p
Are there more cars [y/n]
y
Enter p if car paid the tax and n if it didn't paid the tax
n
Are there more cars [y/n]
y
Enter p if car paid the tax and n if it didn't paid the tax
p
Are there more cars [y/n]
n
Number of cars who paid tax=2
Tax collected =10
Number of cars who didn't paid tax =1
```

After discussing scope of variable, let's discuss storage classes that determine the accessibility of the variable in a program.

## 3.4 Exploring Storage Classes

The storage classes are qualifiers that are used to specify the lifetime of the variable. The lifetime of the variable relates to the portion of the program that has access to the variable. Storage class directs the compiler how you want to store the variable in memory and how you want to access variable within the program. The storage classes are represented with their respective specifiers in C++. Table 1 shows the various storage classes and their respective specifiers:
