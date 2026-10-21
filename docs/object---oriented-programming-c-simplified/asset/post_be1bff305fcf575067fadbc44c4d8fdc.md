
```
12
data =12
```

### EXPLANATION

For the conversion of basic data type to class, a constructor is created which accepts an argument of that data type. Here, we want to convert an int to class demo type. So we have written one argument int type constructor in the class. When statement demo d= num executes compiler automatically calls this one argument constructor with value num. This value num is assigned to data and show function is called which display the data.

### PROG 8.28 DEMO OF TYPE CONVERSION char* TO CLASS TYPE

```cpp
#include <iostream.h>
#include <ctype.h>
#include <string.h>
#include <conio.h>

class demo
{
    char str[20];
public :
    demo(char x[])
    {
        strcpy(str,x);
    }
    int countV()
    {
        int i=0,count=0;
        char ch;
        while(str[i]!=0)
        {
            ch=toupper(str[i]);
            switch(ch)
            {
            case 'A' :
            case 'E' :
            case 'I' :
            case 'O' :
            case 'U' : count++;
            }
            i++;
        }
        return count;
    }
};
void main()
{
    demo d="NMIMS University";
    int c =d.countV();
    clrscr();
    cout<<"Number of vowels = "<<c<<endl;
    getch();
}
```

### OUTPUT

```
Number of vowels = 5
```

### EXPLANATION

For converting a string of char* type to class type we have written a one argument constructor which take argument of type char x[] (Note char* will also do). When demo d = "NMIMS University"; executes string "NMIMS University" is passed to this one argument constructor. The function countV is finding the number of vowels in the string using switch-case. It checks each character from the string str till null character is not encountered. For any of the vowels count is incremented by 1. In the end when string ends count is returned from function.

### PROG 8.29 DEMO OF TYPE CONVERSION FLOAT TO CLASS TYPE

```cpp
#include <iostream.h>
#include <iomanip.h>
#include <conio.h>

class demo
{
    float num;
public :
    demo(float x)
    {
        num = x;
    }
    int int_part()
    {
        return int (num);
    }
    float real_part()
    {
```

```cpp
unsigned long int num;

public :

    CountDigit(unsigned long int x)
    {
        num = x;
    }
    void count()
    {
        int temp [10]= {0};
        int r,i;
        while(num!=0)
        {
            r=num%10;
            temp[r]++;
            num = num/10;
        }
        cout<<"DIGIT \tFREQ\n";
        for(i=0;i<10;i++)
            cout<< i <<"\t" <<temp[i] <<endl;
    }
};

void main()
{
clrscr();
    CountDigit cd=1234567890;
    cd.count();
    getch();
}
```

### OUTPUT

| DIGIT | FREQ |
|-------|------|
| 0     | 1    |
| 1     | 1    |
| 2     | 1    |
| 3     | 1    |
| 4     | 1    |
| 5     | 1    |
| 6     | 1    |
| 7     | 1    |
| 8     | 1    |
| 9     | 1    |

### EXPLANATION

In the program we are finding the frequency of each digit in the unsigned long int number. When statement CountDigit cd = 1234567890; executes one argument constructor which takes an argument of long int type is called and num gets the value 1234567890. The function count() counts the frequency of each digit. For this it uses an array temp size 10. The initial value of each element of this array is 0. In the while loop we are extracting the rightmost digit in turn and incrementing the frequency of that number by 1 using temp array. For this we have made use of % and / operator. This continues till number num does not become zero. For example, if r is 0 in the beginning temp [0] is incremented by 1. Next time temp [9] is incremented by 1 and so on. The maximum limit of unsigned long int 4294967295. Make sure you do not give a number greater than this.

## 2. Conversion from Class Type to Built-in Types

Here we study reverse of what we have studied in the first part. To convert class type to built-in type the method to be adopted is that simply defined an operator function by the name of data type you want class data type to be converted to. The general syntax is :

```cpp
operator data_type ()
{

}
```

Here operator is the keyword we have seen earlier and **data_type** is the type in which your class type will be converted to. The general syntax is :

```cpp
Operator data_type ()
{

}
```

Here operator is the keyword we have seen earlier data_type in which your class type will be converted. Note there is no return type or argument specified for the function. As the above function will be a member function of the class so you can use any data member or function inside this conversion function. You can do any processing over data member as per your requirement but in the end as function is about to return you must return a value of type data_type. For example, assume conversion function is defined in the class demo :

```cpp
operator int ()
{
int x;
computing steps;
return x;
}
```

And in the main it is written int num = d; where d is an object of demo class type. When compiler sees int num = d; it comes to know that both types are not compatible so it look for a conversion routine which can convert an object of demo class type into an int. It finds operator int(). So it calls this conversion function for object d implicitly and assigns the return value to num.

Check out explanatory examples given below :

### PROG 8.31 DEMO OF TYPE CONVERSION, CLASS TO INT

```cpp
#include <iostream.h>
#include <conio.h>
class demo
{
    int num;
public :
    demo(int x)
    {
        num=x;
    }
    operator int()
    {
        return num*num;
    }
};
void main()
{
    int k;
    clrscr();
    cout<<"Enter the number for k :=";
    cin>>k;
    demo d(k);
    int s=d;
    cout<<"Square ="<<s<<endl;
    getch();
}
```

### OUTPUT

```
Enter the number for k : =15
Square =225
```

### EXPLANATION

In the program we have converted an object of demo class type into integer type. When the statement int s=d; executes compiler searches for a function which can convert an object of demo class type to int type. As we have written the function operator int(), this function is called and executes which returns square of num to the s. the square is then displayed. Inside the operator int() you may do whatever you want with the data members of the class but at the end you must return an int type value.

```cpp
class Number
{
    int num;
public :
    Number(int x)
    {
        num = x;
    }
    operator char ()
    {
        if(num<0)
            return 'N';
        else if(num == 0)
            return 'Z';
        else return 'P';
    }
};

void main()
{
    int n;
    clrscr();
    cout << "Enter a number" << endl;
    cin >> n;
    Number d(n);
    char ch = d;
    switch(ch)
    {
        case 'P' :
            cout << "POSITIVE" << endl;
            break;
        case 'N' :
            cout << "NEGATIVE" << endl;
            break;
        case 'Z' :
            cout << "ZERO" << endl;
            break;
    }
    getch();
}
```

### OUTPUT

```
(First run)
Enter a number
23
POSITIVE

(Second run)
Enter a number
-23
NEGATIVE
(Third run)
Enter a number
0
ZERO
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_400_0.png)

Figure 8.2. Output screen of first, second and third run of program 8.33

### EXPLANATION

In the program we are converting an object of demo class type to char. The function operator char () checks num for positive, negative or zero and return `P`, `N` and `Z` respectively. This returned character is stored in ch variable in main which is put into the switch. Depending upon the value of ch appropriate result is displayed.

### PROG 8.34 DEMO OF TYPE CONVERSION, CLASS TO CHAR*

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>
class Rev
{
    char str[25];
public :
    Rev()
    {
        cout<<"ENTER A STRING "<<endl;
        cin.getline(str,25);
    }
    operator char*();
};

Rev ::operator char*()
{
    static char s[25];
    strcpy(s,strrev(str));
    return s;
}
void main()
{
    clrscr();
    Rev R;
    char *t = R;
    cout<<"Reverse String is "<<t<<endl;
    getch();
}
```

### OUTPUT

```
ENTER A STRING
NMIMS UNIVERSITY
Reverse String is YTISREVINU SMIMN
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_401_0.png)

Figure 8.3. Output screen of program 8.34

### EXPLANATION

Rev R creates object R by calling default constructor of the class. The default constructor prompts user for the string. Assume string is "NMIMS UNIVERSITY". When char *t=R executes, function operator char*() called automatically. Inside the function we have reversed the string with the help of strrev function courtesy string.h. Note inside the function we have used static array as return address of a local variable will result in garbage value. The returned reverse string is stored in t which is displayed.
