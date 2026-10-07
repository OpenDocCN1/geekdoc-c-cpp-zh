increment is to increase by one; it is the opposite of decrement, and unrelated to exemment., which is a noun.) When we exit the loop, count contains the result: the total number of a's.

As an exercise, encapsulate this code in a function named countLetters, and generalize it that it accepts the string and the letter as arguments.

As a second exercise, rewrite this function that instead of traversing the string, it uses the version of find we wrote in the previous section.

# 7.10 Increment and decrement operators

Incrementing and decrementing are such common operations that C++ provides special operators for them. The ++ operator adds one to the current value of an int, char and -- subtracts one. Neither operator works on apstrings, and neither should be used on bools.

Technically, it is legal to increment a variable and use it in an expression at the same time. For example, you might see something like:

```
cout << i << endl;
```

Looking at this, it is not clear the increment will take effect before or after the value is displayed. Because expressions like this tend to be confusing, I discourage you from using them. In fact, to discourage you even more, I'm not going to tell you what the result is. If you really want to know, you can try.

Using the increment operators, we can rewrite the letter-counter:

```
int index = 0;
while (index < length) {
  if (fruit[index] == 'a') {
    count++;
  }
  index++;
}
```

It is a common error to write something like

```
index = index++; // WRONG!
```

Unfortunately, this is syntactically legal, so the compiler will not warn you. The effect of this statement is to leave the value of index unchanged. This is often a big bug to track down.

Remember, you can write index = index+1; or you can write index++; but you shouldn't mix them.