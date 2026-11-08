You can compile and execute this program to verify that the `increase` function changes the value of the variable named `new_salary`. The program, named `IncreaseSalary.cpp`, is included with the data files provided with this book.

# PASS BY ADDRESS

The second technique you can use to pass the memory address of variables (that are not arrays) to functions is called pass by address. Passing an argument by address allows the called function to change the value of an argument.

Before you can understand passing arguments by address, you must learn about pointers. A **pointer** is a variable that stores a memory address as its value. You are accustomed to using a variable name to directly access a value stored at a memory address associated with a variable. You can also use a pointer variable and the memory address stored in the pointer variable to indirectly access a value stored at a memory address.

The first thing you need to learn in order to use pointers is how to use the address operator. You use the C++ address operator `&` to obtain the memory address associated with a variable. The following C++ code prints the value of a variable named `num` and also uses the address operator `&` to print the memory address associated with the variable named `num`:

```
```cpp
int num = 5;
cout << "Value of num is: " << num << endl;
cout << "Address of num is: " << &num << endl;
```
```

As you can see in the preceding, highlighted line of code, the address operator (`&`) is placed before the name of the variable (`num`) to obtain the address of num.

Next, you must learn to use the `*` symbol to declare a pointer variable. When you declare a pointer, a specific data type must be explicitly associated with the pointer. The C++ code that follows declares an `int` variable named `age` and `ptr_age` as a pointer to an int:

```
```cpp
int age = 21;
int* ptr_age = &age;
```
```

Figure 7-8 shows memory after the preceding code executes. The variable named age is associated with memory location 2000, where the value 21 is stored. The variable named ptr_age is associated with memory location 2004 where the value 2000 (the address of the int age) is stored. Because ptr_age contains the address of age, you can say that ptr_age is a pointer to an int and that it points to age.

![](bbox=[0.214, 0.774, 0.489, 0.889])

**Figure 7-8** Memory contents for age and ptr_age