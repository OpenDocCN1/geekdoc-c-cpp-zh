(x + 2) = y / 2  
x + 4 = y  
solve for x and y

If you are any good at algebra you may have already solved the problem. However, simply inputting this information into C++ is not enough for the program to understand what this all means. It will read it only as gibberish and it will make no sense at all to the computer. This is why we must *declare* our variables to the program before we can use it, so that the computer knows exactly what we are trying to do. So we would declare our variables by:

```
```cpp
int x;
x = 10;

int y;
y = 5;
```
```

As we have seen in the previous chapter, the statement “int” basically means “start”. Here, we are saying that x equals 10 and y equals 5. If we were then to write the code again, the program would be able to solve the problem. We can use these variables anywhere that we like in the program, but we must always declare to the system what they mean before we can use them. And it is not only numbers that we can store in the variables. We could also use the following:

```
```
x = 1
x = 2.3
x = “this is a sentence”
```
```

To give you a further example of how variables work, consider the following. I tell you to remember the number 5 and the number 2. You have just stored two values in your mind. I then tell you to add the number 1 to the first number which I said. Now, in your memory, you should have the number 6 (5+1) and the number 2. I then ask you to subtract the first number from the second and then we get the answer of 4.

This basically explains how C++ will store variables and then use them to solve problems or statements. When actually writing it in code, it would look like this: