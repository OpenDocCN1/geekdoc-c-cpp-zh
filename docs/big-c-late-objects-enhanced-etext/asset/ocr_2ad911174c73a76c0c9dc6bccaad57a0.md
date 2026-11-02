![](bbox=[0.12, 0.12, 0.92, 0.36])

# Figure 1 Pointers and Values in Memory

A pointer denotes the location of a variable in memory.

The type T* denotes a pointer to a variable of type T.

The & operator yields the location of a variable.

Here is the definition of a pointer variable. The pointer variable is initialized with the location (also called the address) of the variable harrys_account (see Figure 1):

```
double* account_pointer = &harrys_account;
```

The type double*, or "pointer to double", denotes the location of a double variable. The & operator, also called the address operator, yields the location of a variable. Taking the address of a double variable yields a value of type double*.

Thinking about pointers can be rather abstract, but you can use a simple trick to make it more tangible. Every variable in a computer program is located in a specific memory location. You don't know where each variable is stored, but you can pretend you do. Let's pretend that harrys_account is stored in location 20300. (That is just a made-up value.) As shown in Figure 1, the value of harrys_account is 0, but the value of &harrys_account is 20300. The value of account_pointer is also 20300. In our diagrams, we will draw an arrow from a pointer to the location, but of course the computer doesn't store arrows, just numbers.

By using a pointer, you can switch to a different account at any time. To access a different account, simply change the pointer value:

```
account_pointer = &joint_account;
```

# 7.1.2 Accessing Variables Through Pointers

The * operator accesses the variable to which a pointer points.

When you have a pointer, you will want to access the variable to which it points. The * operator is used to read or update the variable to which a pointer points. When used with pointers, the * operator has no relationship with multiplication. In the C++ standard, this operator is called the indirection operator, but it is also commonly called the dereferencing operator.

This statement makes an initial deposit into the account to which account_pointer points (see Figure 2):

```
*account_pointer = 1000;
```