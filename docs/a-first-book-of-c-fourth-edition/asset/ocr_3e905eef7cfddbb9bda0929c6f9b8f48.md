# 2. a.

| Variable or Constant Name | Data Type | Scope |
|---|---|---|
| KEY | char | global to main(), func1(), and func2() |
| NUMBER | long int | global to main(), func1(), and func2() |
| a, b, c | int | local to main() |
| x, y | double | local to main() |
| secnum | double | global to func1() and func2() |
| num1, num2 | int | local to func1() |
| o, p | int | local to func1() |
| q | float | local to func1() |
| first, last | double | local to func2() |
| a, b, c, o, p | int | local to func2() |
| r | double | local to func2() |
| s, t, x | double | local to func2() |

3. All function parameters have local scope in their defined function. Note that although function parameters assume a value that depends on the calling function, these parameters can change values in their functions. This makes them behave as though they were local variables in the called function.

# EXERCISES 6.5

1. a. The storage categories available to local variables are auto, static, and register.

b. The storage categories available to global variables are extern and static. A local auto variable is unique to the function in which it's declared. Every time the function is called, the auto variable is re-created, as though it never existed. A local static variable is also unique to the function where it's declared. However, a static variable retains its last value and isn't re-created when its function is called again.

2. The first function declares yrs to be a static variable and assigns a value of 1 to it only once, when the function is compiled. Each time the function is called thereafter, the value in yrs is increased by 2. The second function also declares yrs to be static but assigns it the value 1 every time it's called, and the value of yrs after the function is finished will always be 3. By resetting the value of yrs to 1 each time it's called, the second function defeats the purpose of declaring the variable to be static.