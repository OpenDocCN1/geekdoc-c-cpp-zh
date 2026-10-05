Explanation: A simple practice question on call by reference.
Explanation is not required.

29. b

Explanation: Implicit type conversion is supported by gcc compiler. The integer pointer first get converted into a float pointer implicitly and then in fun(), the float pointer gets typecast into an integer pointer explicitly. The value at the address of 'i' that is 10 will be printed.

30. a

Explanation: Not required.

31. c

Explanation: A simple concept of double-pointer. We already discussed these questions.

32. d

Explanation: The functional argument in fun() int *const*p; //*p is constant (that is read-only) but we tried to update it at line 2. Hence, the compiler throws an error.

33. c

Explanation: The program will run fine, here, 'p' is constant in fun(). We are updating *p, that is possible.

34. c

Explanation: Here, we cannot update 'a' in function main(). With the help of pointers, it is possible to update const variables also, like here, we are updating 'a' in fun(). This is also called "Variable Hacking". If we want to prevent the variable hacking, just change the prototype of function fun() to void fun(const *p).

35. b

Explanation: One more example of variable hacking.

36. d

Explanation: A given array 'a' is constant, a[3] = 78; is an invalid operation.

37. b