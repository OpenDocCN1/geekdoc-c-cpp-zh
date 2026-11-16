
## Hello World

See, here \b moves the cursor back to character 'c' and then we overwrite c with a space. We can also overwrite any character by space.

### Consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Helloc\b World";
}
```

### Output

Hello World

Here, we have left a space just after \b and so c is overwritten with space and we get our desired output Hello World.

## \f Formfeed

This character is negligibly used in programs but it is widely used if a printer or word file is involved. This character signals the OS that the current form has ended and it is time to start a new form. But, in program output it only displays the character that plays this role for a printer or file. So, if we want to insert a new page in a word file through a program, we use \f there. Since most books cover only text files and binary files, they do not tell you about this.

To verify what we have learnt here, after studying about files, come here and run the following program:

```cpp
#include<iostream>
#include<fstream>
using namespace std;
int main()
{
    fstream fout;
    fout.open("A.doc", ios::out);

    if(!fout)
    {
        cout<<"Can't open";
        return -1;
    }

    fout<<"Hello World\fHello World";

    fout.close();
}
```

Here, a file A.doc will be created and written. When you open A.doc, you will see Hello World written on two different pages. This confirms that the character \f separates the forms.

![](img/5340985153962870d4e4a3b9453b9146_31_0.png)

## \n Newline

This character is for line feed, i.e., whatever we write after this character is written on a new line. Consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello\nWorld";
}
```

### Output

Hello

World

Here, Hello and World will be displayed on different lines.

## \r Carriage return

This is not like \n. The problem with people is that they are generally never explained where to use \r. So they ask many questions about its use on forums. Well, \r moves the cursor to the beginning of the current line being displayed. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello world\rBlack";
}
```

### Output:

Black world

See, here after printing Hello World, the cursor moves to the beginning of the line, and then since it has to write Black, it overwrites it with Black. Now you have understood that \r is something like \b but not like \n at all. You can also say this is equivalent to the Home button on our keyboard.

## \t Tab

This is used to leave a tab space on the output screen. A tab space is generally equal to five spacebars. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello world\tBlack";
}
```

### Output

Hello world   Black

This is generally used to create a menu bar on the output screen. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"1.File\t2.Edit\t3.View\t4.Search\t5.Exit";
}
```

### Output

1.File   2.Edit   3.View   4.Search   5.Exit

## Various uses of backslash

Suppose we are illustrating \b to someone, and we have to display \b and not its effect. You may think that `cout<<"\b";` will display \b, but then you will realize that it will instead try to move the cursor one step backward. So, how to print \b? The solution is to use a double backslash. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"\\b";
    cout<<"\\n";
    cout<<"\\n";
    cout<<"\\n";
    cout<<"\\"";
}
```

### Output

\b



"

See here, to print a single apostrophe, double apostrophe, and backslash, we have to use a backslash before them.

## puts() function

puts() is a function used to print string output and then place a line feed. This function is defined in stdio.h. So, if at compile time the compiler gives an error that puts() should have a prototype or puts() is undeclared, then just add `#include<stdio.h>` at the beginning of the program. All latest compilers include this function in iostream too.

For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    puts("Aman");
    puts("Kumar");
}
```

### Output:

Aman
Kumar

Here, Aman and Kumar will be printed on separate lines instead of using the newline character. This is one of the features of puts().

## cout.put()

This function places a character on the screen. Unlike puts(), it does not insert any line feed. Consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout.put('a');
    cout.put('k');
}
```

### Output:

ak

Now, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout.put('a').put('k');
}
```

### Output:

ak

This program shows that .put() can be cascaded multiple times.

## cout.write()

This is used to display a particular number of bytes on the output screen. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout.write("Aman Kumar Jha", 7);
}
```

### Output:

Aman Ku

Here, only the initial seven bytes of the string passed will be displayed.

## endl

This macro produces a newline character, exactly like inserting `\n`, but it also has an additional behavior when used with buffered streams: the buffer is flushed. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello"<<endl;
    cout<<"world";
}
```

### Output

Hello

world

See, the use of endl is shown in the line above. Consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<"Hello"<<endl<<"world";
}
```

This program will have the same output as the previous one.

## oct, dec, hex

These are some of the macros used to display the octal and hexadecimal values of a variable or constant. For example, consider the following program:

```cpp
#include<iostream>
using namespace std;
int main()
{
    cout<<17<<endl;
    cout<<oct<<17<<endl;
    cout<<hex<<17<<endl;
    cout<<dec<<17;
}
```

### Output

17
21
11
17

These macros also work fine with functions. After reading the functions chapter, come here and see the following program:

```cpp
#include<iostream>
using namespace std;
int add(int, int);
int main()
{
    cout<<add(5, 6)<<endl;
    cout<<oct<<add(5, 6);
}

int add(int a, int b)
{
    return a + b;
}
```

### Output
11
13

## iomanip.h

This is a header file used for input/output manipulation. We shall include it for various purposes. It includes various functions, macros, and classes. Some of them are very useful, and we shall discuss them.

- setprecision()
- setbase()
- setw()

### setbase()

setbase() is an alternative to the three different macros oct, dec, and hex.

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int main()
{
    cout<<setbase(8)<<17<<endl;
    cout<<setbase(10)<<17<<endl;
    cout<<setbase(16)<<17;
}
```

### Output
21
17
11

Any number cannot be passed as an argument to setbase(), as it will display only octal, decimal, or hexadecimal values, so only 8, 10, 16 can be used.

### setprecision()

It is used to set the precision points. Suppose you have a value, say 21.23456789, and you want to display this number up to five digits; then the program will be:

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int add(int, int);
int main()
{
    float a = 21.23456789;
    cout<<setprecision(5)<<a;
}
```

### Output
21.345

Now, think about what the output will be if we try to set the precision point to less than 2. See the following program:

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int add(int, int);
int main()
{
    float a = 21.23456789;
    cout<<setprecision(1)<<a;
}
```

### Output
2e+001

So, it starts converting the number to scientific notation as the value in setprecision() decreases. However, using it we cannot decide the number of digits to display after the decimal point using rounding. Here, setw() is used.

### setw()

This function allows us to display a fixed number of digits after the decimal point with rounding. For example, consider the following program:

```cpp
#include<iostream>
#include<iomanip>
using namespace std;
int add(int, int);
int main()
{
    float a = 21.23456789;
    cout<<setw(4)<<a;
}
```

### Output
21.2346
