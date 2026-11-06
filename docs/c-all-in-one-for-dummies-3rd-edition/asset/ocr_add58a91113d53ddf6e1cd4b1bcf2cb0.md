![](bbox=[0.882, 0.135, 1.0, 0.304])

going to be true. When x is −50, it’s less than 100, so the condition is true. When x is 500, it’s greater than 0, so it’s true. In addition to an or situation, you can have something like this: “If I get a million dollars and I feel really bold, then I will buy a Lamborghini.” Notice that we’re using the word **and**. In this case, you do it only if both situations are true. (Remember that with **or**, you do it if either situation is true.) In C++, the **and** operator is two ampersands: `&&`. This makes more sense than the **or** operator because the ampersand is often associated with the word **and**. The **and** operator in C++ looks like this:

```
```cpp
{i > 10 && i < 100}
```
```

This example checks to see whether a number is more than 10 and less than 100. That would mean the number is in the range 11 through 99.

Combining conditions by using the `&&` and `||` operators is a use of *logical operators*.

To determine whether a number is within a certain range, you can use the *and* operator (`&&`), as we do earlier in this chapter.

![](bbox=[0.12, 0.403, 0.209, 0.548])

With the *and* operator, accidentally creating a condition that is never true is easy. For example, the condition `(x < 10 && x > 100)` will never be true. No single number can be both less than 10 and simultaneously greater than 100.

# Including Evaluations in C++ Conditional Statements

Computers, like humans, evaluate conditions and use the results of the evaluations as input for making a decision. For humans, the decision usually involves alternative plans of action, and the same is true for computers. The computer needs to know what to do if a condition is true and what to do if a condition is not true. To decide on a plan of action based on a condition that your application evaluates, you use an `if` statement, which looks like this:

```
```cpp
if (x > 10)
{
    cout << "Yuppers, it’s greater than 10!" << endl;
}
```
```

This example translates into English as: If x is greater than 10, write the message

```
```cpp
"Yuppers, it’s greater than 10!"
```
```

In an `if` statement, the part inside the parentheses is either the *test* or the *condition*. We usually apply *condition* to this part of the `if` statement and use the word *test* as a verb, as in “I will test whether x is greater than 10.”