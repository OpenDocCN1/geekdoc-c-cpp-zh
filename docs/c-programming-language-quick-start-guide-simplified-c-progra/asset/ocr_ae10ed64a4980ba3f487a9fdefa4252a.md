might have hardware based restrictions since there are a limited number of registers in physical space. Because of physical restrictions, variables of this class are automatically converted to auto type whenever compiler finds it impossible to use the variable as a memory register.

Register class is used when fast execution is critical. When speed is a concern, the programmer may choose a few variables that are frequently accessed and declare them to be of storage class register. Registers take lesser number of clock cycles when they are accessed for use or modification than normal memory location. Since registers store integer values, hence extern variables are integer by default as well. Therefore following two declarations are equivalent:

```
extern int variable;
extern variable;
```

# 3.4.4 Storage Class static

Static means something which keeps its state constant. Static class have two basic uses.

The primary use is similar to what the word static means: for declaring variables which