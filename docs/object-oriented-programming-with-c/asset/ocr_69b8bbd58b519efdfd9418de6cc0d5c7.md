The double slash comment is basically a single line comment.
Multiline comments can be written as follows:

```
```cpp
// This is an example of
// C++ program to illustrate
// Some of its features
```
```

The C comment symbols /*, */ are still valid and are more suitable
for multiline comments. The following comment is allowed:

```
```cpp
/* This is an example of
   C++ program to illustrate
   some of its features
*/
```
```

We can use either or both styles in our programs. Since this is a
book on C++, we will use only the C++ style. However, remember
that we can not insert a // style comment within the text of a program
line. For example, the double slash comment cannot be used in the
manner as shown below:

```
```cpp
for(j=0; j<n; /* loops n times */ j++)
```
```

# Output Operator

The only statement in Program 2.1 is an output statement. The
statement

```
```cpp
cout << "C++ is better than C."
```
```

causes the string in quotation marks to be displayed on the screen.
This statement introduces two new C++ features, cout and <<. The
identifier cout (pronounced as ‘C out’) is a predefined object that
represents the standard output stream in C++. Here, the standard
output stream represents the screen. It is also possible to redirect the
output to other output devices. We shall later discuss streams in
detail.