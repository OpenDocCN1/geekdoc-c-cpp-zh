```
```c
3  int main()
4  {
5  int age;
6
7  age = 30;
8  printf("The C language is over %d years old!\n", age); 9
10 return(0);
11 }
```
```

This code declares an integer variable at line five. First comes the keyword which is used to declare an integer variable. Next come the variable name: age. As this is a statement, it ends with a semi-colon. Variable names can include numbers, letters, and some symbols. They must begin with a letter, or an underline. The name must be unique, with no two variables having the same name, nor should variables have the same name as functions or C language keywords.

At line seven, the variable *age* is assigned the value 30. In C, values or equations go on the right side of the assignment operator, the equal sign. The value or results of the equation is then assigned to the variable on the left. Because 30 is an integer value, it fits nicely into the integer variable

The statement at line nine displays the variable’s value by using the *printf* function. The %d placeholder is used, and the variable *age* is specified as the second argument. Now go ahead and build and run the code. The whole idea behind the variable is that its value can change. Edit the source code so that the value of the *age* variable is changed to 34. Make this modification at line seven.

```
```c
1  #include 2
```
```