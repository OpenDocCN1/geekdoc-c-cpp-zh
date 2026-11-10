**Format string** It is a group of characters that contain ordinary character string, conversion code, or control characters arranged in order so that they correspond to the respective control string variables placed next to it in printf() function.

**Precision modifier** It indicates the number of characters used after the decimal point in the output displayed. The precision option is used only with floats or strings.

**Size modifier** It precedes the conversion code and specifies the kind of data type thereby indicating the number of bytes required for the corresponding variable.

**White space** It is the blank space that causes the input stream to be read up to the next non-white-space character.

**Width modifier** When used in context with the format string, with modifier specifies the total number of characters used to display the output or to be read in.

# **FREQUENTLY ASKED QUESTIONS**

**1. How can you print % character using printf()?**
Conversion specifiers always start with a % character so that the printf() function can recognize them. Because a % in a control string always indicates the start of a conversion specifier, if one wants to output a % character you must use the sequence %%.

**2. What is the return type of printf()?**
The return value for printf() is incidental to its main purpose of printing output, and it usually isn't used. The return type of printf() function is int. Under ANSI C, printf() function returns the number of characters it printed. If there is an output error, printf() returns a negative value. The following program illustrates the fact:

```
```c
#include <stdio.h>
int main(void)
{
   int c;
   c=printf("One");
   printf("\nc = %d",c);
   return 0;
}
```
```

Output
One
c = 3

**3. What is the return type of scanf()?**
The scanf() function returns the number of variables that it successfully reads. If it reads no variables, which happens if you type a non-numeric string when it expects a number, scanf() returns the value 0. It returns EOF if it detects end of file. This condition can occur if we press CTRL-Z in Windows or CTRL-D in UNIX/Linux.

```
```c
#include <stdio.h>
int main(void)
{
   int a,b,c;
   c=scanf("%d %d",&a,&b);
   printf("\nc = %d",c);
   return 0;
}
```
```

```
```
Output
Sample run 1:
2 3
c = 2

Sample run 2:
2 a
c = 2

Sample run 3:
a b
c = 0

Sample run 4:
^z
c = -1
```
```

**4. How do I write printf() so that the width of a field can be specified at run-time?**
This is shown in the following program:

```
```c
int main( )
{
   int w, no;
   printf ("Enter number and the width for the\
number field:");
   scanf ("%d%d", &no, &w);
   printf ("%*d", w, no);
   return 0;
}
```
```

Here, * in the format specifier in printf() indicates that an int value from the argument list should be used for the field width.

**5. What is EOF?**
EOF is a special character called the end-of-file character. In fact, the symbol EOF is defined in <stdio.h> and is usually equivalent to the value -1. However, this is not necessarily always the case, so one should use EOF in the programs rather than an explicit value. EOF generally indicates that no more data is available from a stream. Incidentally EOF can be entered manually from the keyboard by pressing CTRL+D on a UNIX/Linux type machine or by pressing CTRL+Z on a Windows type machine.

# **EXERCISES**

**1. What will be the value of each variable after the following input command?**
data input: Tom 34678.2 AA4231

scanf("%s %3d %f %c %c %ld", name, &m, &x, &ch, &i, &j);
(a) name: ___________________________