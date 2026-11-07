```
~~~cpp
int main()
{
    int miles;

    try
    {
        cout << "Enter the miles: ";
        cin >> miles;
        cout << endl;

        if (miles < 5)
            throw tornadoException();
        else
            throw tornadoException(miles);
    }
    catch (tornadoException tE)
    {
        cout << tE.what() << endl;
    }

    return 0;
}
~~~
```

+   23. A function specifies the exceptions it throws in its heading using the throw clause.
+   25. (1) Do nothing; (2) Partially process the exception and throw the same exception or a new exception; (3) Throw a new exception.

# # Chapter 15

+   1. a. true; b. true; c. false; d. false; e. false; f. false; g. true; h. true
+   3. The case in which the solution is defined in terms of smaller versions of itself.
+   5. A function that calls another function and eventually results in the original function call is said to be indirectly recursive.
+   7. a. The statements in Lines 2 and 3.
+      b. The statements in Lines 4 and 5.
+      c. Any nonpositive integer.
+      d. It is a valid call. The value of mystery(0) is 0.
+      e. It is an invalid call. It will result in infinite recursion.
+      f. It is a valid call. The value of mystery(-3) is 6.
+   9. a. 8 5 2  b. 7  c. 6 3  d. -85
+   11. a. It does not produce any output.
+       b. 5 6 7 8 9
+       c. It does not produce any output.
+       d. It does not produce any output.