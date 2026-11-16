
See here, last decimal digit has been rounded. Rounding rule is pretty simple, if the last digit which is to be rounded has the digit greater than 4, next to it then the last digit is not changed else it is increased by 1.

## cin ( >> )

whenever, we want to take an input from keyboard, we use cin class with right shift operator (>>).e.g. Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int a;
    cout<<"Enter a number\n";
    cin>>a;
    cout<<"The number you entered is "<<a;
}
```

Output

Enter a number

5

The number you entered is 5

Here, you can see that cin takes the input without clarifying the type of input.

## Cascading input

Cin also supports cascading inputs. So, in the following program we have tried to input one number and a character through one line.

```
#include<iostream>
using namespace std;
int main()
{
    int a;
    char ch;
    cout<<"Enter a number and a character\n";
    cin>>a>>ch;
    cout<<"The number you entered is "<<a<<" and the character is "<<ch;
}
```

### Output

Enter a number and a character
5
c
The number you entered is 5 and the character is c

You may think that, it means it can take any of input but it is not the fact. It is not as much data type independent as cout. Following program is an attempt to input a number, a character, a string, see what happens:

```
#include<iostream>
using namespace std;
int main()
{
 int a;
 char b;
 char c[50];
 cout<<"Enter a number\n";
 cin>>a;
 cout<<"Now enter a character\n";
 cin>>b;
 cout<<"Now enter a string\n";
 cin>>c;
 cout<<"The number you entered is "<<a<<endl;
 cout<<"The character you entered is "<<b<<endl;
 cout<<"The string you entered is "<<c<<endl;
}
```

### Output

```
Enter a number
5
Now enter a character
s
Now enter a string
word is word
The number you entered is 5
The character you entered is s
The string you entered is word
```

This program clears that we can only insert a word with cin not a string. So, then how to input a string, fret not there are various others options let us see those options one by one.

## gets()

This function is used to get a string. This function is defined in stdio.h. So, if at compiler time the compiler gives you an error gets() should have a prototype or gets() undeclared, then just use one more sentence #include<stdio.h> at the beginning of the program. All latest compilers, include this function in iostream too.

E.g. Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    char ch[100];
    cout<<"Enter a string\n";
    gets(ch);
    cout<<"Entered string is "<<ch;
}
```

### Output

Enter a string

word is word

Entered string is word is word

## cin.get()

This function is used to take a character as input from screen. E.g. consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    char ch;
    cout<<"Enter a character\n";
    cin.get(ch);
    cout<<"Entered character is "<<ch;
}
```

### Output

Enter a character

5

Entered character is 5

## cin.getline(char*,int l,char f)

This function is used to take a line as input from screen.

It is a overloaded function, means it can be used with two arguments as well as three arguments. First argument is the char pointer to which the line is stored. Second argument is the number of characters to store. Third argument is optional, it is called delim character. Suppose you want to input the characters until a particular character strikes. That particular character can be used as a delimit character. If the delimitative character is used then second argument and third argument both should be responsible for terminating the input process. In that case, whichever strikes earlier out of second and third argument, is used to terminate the input process.

E.g, consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    char ch[50];
    cout<<"Enter a line\n";
    cin.getline(ch,50);
    cout<<"Entered line is: "<<ch;
}
```

### Output

Enter a line

I am Aman

Entered line is: I am Aman

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    char ch[50];
    cout<<"Enter a line\n";
    cin.getline(ch,50,'*');
    cout<<"Entered line is: "<<ch;
}
```

### Output

Enter a line

I am A*man

Entered line is: I am A

See here, * is used as delimitative character.

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    char ch[50];
    cout<<"Enter a line\n";
    cin.getline(ch,5,'*');
    cout<<"Entered line is: "<<ch;
}
```

### Output

Enter a line

I am Am*am

Entered line is: I am

See here, out of second argument and third argument, second argument strikes earlier as it is telling the function to store only five characters, while * is at eighth character.

## cin.read(unsigned char*,int l)

This function is used to take a fixed number of inputs from the screen; this is very useful while dealing with the big data which can even cause the buffer overflow attacks. Following is a program which shows the use of cin.read():

```
#include<iostream>

using namespace std;

int main()
{
    char ch[100];
    cout<<"Enter a string\n";
    cin.read(ch,7);
    cout<<"Entered string is "<<ch;
}
```

### Output

Enter a string
Word is word
Entered string is Word is
See here, we entered 11 characters, but only 7 characters is accepted.

## oct, dec, hex

Like as in cout, these macros are used in input too but even more amazingly. E.g. Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int num;
    cout<<"Enter a number\n";
    cin>>hex>>num;
    cout<<"Entered number is "<<num;
}
```

### Output

Enter a number

Entered number is 23

See, the number we gave as input was treated as hexadecimal and so the corresponding decimal value has been printed. Similarly see the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int num1,num2;
    cout<<"Enter a number\n";
    cin>>hex>>num1;
    cout<<"Enter another number\n";
    cin>>oct>>num2;
    cout<<"Entered numbers are "<<num1<<" "<<num2;
}
```

### Output

Enter a number
23
Enter another number
45
Entered numbers are 35 37

## setbase()

setbase() can be used to input both octal and hexadecimal number.

```
#include<iostream>
#include<iomanip>
using namespace std;

int main()
{
    int a;
    cout<<"Enter a number\n";
    cin>>setbase(8)>>a;
    cout<<a;
}
```

### Output

Enter a number
17
15

See, like we used setbase() function with cout class, in the same manner setbase() can be used with cin also.

## Increment & decrement operator (++ & --)

This is a very important operator. It has following types:

- 1.Preincrement: ++variable_name : This operator increases the value by one then starts calculation
- 2.Predecrement: --variable_name: This operator decreases the value by one then starts calculation
- 3.Postincrement: variable_name++: This operator first calculates then increases the value by one
- 4.Postdecrement: variable_name--: This operator first calculates then decreases the value by one

Consider the following example:

```
#include<iostream>
using namespace std;
int main()
{
int a=5;
cout<<a++<<endl;
cout<<a;
}
```

### Output

5
6

Here, at first it displays the value stored in a which is 5 then it increases its value by one and now the value in a is 6. So, when we print a second time, it displays 6.

Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    int a=5;
    cout<<++a<<endl;
    cout<<a;
}
```

### Output

6
6

Here, at first value in a is increased by one then the value stored in a is printed.

Now, consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
int a=5;
cout<<++a<<" "<<a<<" "<<a++;
}
```

### Output

7 7 5

To solve such types of programs, at first we calculates the values from right to left. For all those expressions which involves ++ or – operator, the value is whatever we got from calculation. So, in the above problem, we get the value of two of the expression 7, 5. Now, to get the value of a, the value which is finally stored while calculating from right to left is taken, so from right to left at first value stored in a is 5, which is post incremented in right most expression, now in middle expression this value has not been changed and in leftmost expression, this value is increased to 7, by preincrement operation. So, the final value stored in a is 7. So, the value which is displayed for 2nd expression will be 7. So, 7 7 5 has been displayed.

The whole logic explained above works same for –operator.

## Type casting

Converting one type of variable to another type is called type casting. Type can be both automatic and manual. Consider the following program

```
#include<iostream>
using namespace std;
int main()
{
int a=255;
float b=182;
char d=a-b;
cout<<d;
}
```

This program may seem incorrect, but there is no error in this program. Since d=a-b=255-182-73,so the ASCII character of 73 which is capital i will be stored in d. So, output will be printed as I
