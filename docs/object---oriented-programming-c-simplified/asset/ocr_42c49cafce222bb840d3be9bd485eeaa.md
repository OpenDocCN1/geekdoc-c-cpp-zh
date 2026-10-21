```
```cpp
cout << “Enter the last name := ”;
cin >> lname;

cout << “Your full name := ”;
ostream & refcout=cout.write(fname, strlen(fname));

refcout.write(“ ”, 1);
refcout.write(lname,strlen(lname));
cout << endl;

getch( );
}
```
```

# **OUTPUT :**

Enter first name : = HARI  
Enter the last name : = PANDEY  
Your full name : = HARI PANDEY

**EXPLANATION :** The statement given below as :

```
```cpp
ostream & refcout=cout.write(fname, strlen(fname));
```
```

First display fname onto the screen and then returns reference of ostream type which is stored in refcout. In the next statement we use this refcout to display lname using write method. The whole of the write statements can be written in the shorter form as:

```
```cpp
cout.write(fname, strlen (fname))
Write(“ ”,1).write (lname,strlen(lname));
```
```

# 11.4 FORMATTED INPUT/OUTPUT OPERATIONS

In C++ for formatting input and output we have three methods :

+   1. Use of functions and flags defined by ios class.
+   2. Use of manipulators (built-in)
+   3. User defined manipulators.

# 1. Use of Functions and Flags Defined by ios Class

# A. ios Function and Flags

The class ios provides number of formatting functions for input and output. The most frequently used are listed below :

# (a) The width ( ) Function

The function is used to set the width *i.e.*, field size for displaying a data value of type numeric or string. The syntax of this is as follows :