doubleNumber module, which causes the number variable’s contents to be copied into the value parameter variable. This is shown in Figure 3-13.

# Program 3-6

```
Module main()
  Declare Integer number
  Display "Enter a number and I will display"
  Display "that number doubled."
  Input number
  Call doubleNumber(number)
  End Module

Module doubleNumber(Integer value)
  Declare Integer result
  Set result = value * 2
  Display result
  End Module
```

# Program Output (with Input Shown in Bold)

Enter a number and I will display
that number doubled.
20 [Enter]

Figure 3-13 The contents of the number variable passed as an argument

![](bbox=[0.247, 0.566, 0.742, 0.783])

# Argument and Parameter Compatibility

When you pass an argument to a module, most programming languages require that the argument and the receiving parameter be of the same data type. If you try to pass an argument of one type into a parameter of another, an error usually occurs. For example, Figure 3-14 shows that you cannot pass a real number or a Real variable into an Integer parameter.