![](bbox=[0.16, 0.1, 0.92, 0.35])

The type double*, or “pointer to double,” denotes the location of a double variable. The & operator, also called the address operator, yields the location of a variable. Taking the address of a double variable yields a value of type double*.

The type T* denotes a pointer to a variable of type T.

Thinking about pointers can be rather abstract, but you can use a simple trick to make it more tangible. Every variable in a computer program is located in a specific memory location. You don’t know where each variable is stored, but you can pretend you do. Let’s pretend that we know that harrys_account is stored in location 20300. (That is just a made-up value.) As shown in Figure 1, the value of harrys_account is 0, but the value of &harrys_account is 20300. The value of account_pointer is also 20300. In our diagrams, we will draw an arrow from a pointer to the location, but of course the computer doesn’t store arrows, just numbers.

The & operator yields the location of a variable.

By using a pointer, you can switch to a different account at any time. To access a different account, simply change the pointer value:

```
`account_pointer = &joint_account; ②`
```

# ### 7.1.2 Accessing Variables Through Pointers

The * operator accesses the variable to which a pointer points.

When you have a pointer, you will want to access the variable to which it points. The * operator is used to read or update the variable to which a pointer points. When used with pointers, the * operator has no relationship with multiplication. In the C++ standard, this operator is called the indirection operator, but it is also commonly called the dereferencing operator.

This statement makes an initial deposit into the account to which account_pointer points (see Figure 2):

```
`*account_pointer = 1000; ①`
```

In other words, you can use *account_pointer in exactly the same way as harrys_account or joint_account. Which account is used depends on the value of the pointer. When the program executes this statement, it fetches the address stored in account_pointer. It then uses the variable at that address, as shown in Figure 2.