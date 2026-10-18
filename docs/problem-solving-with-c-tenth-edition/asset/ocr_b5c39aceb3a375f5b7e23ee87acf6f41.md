```
int number = 22;
{
    int number = 42;
    cout << number << " ";
}
cout << number;
```

20. Though we urge you not to program using this style, we are providing an exercise that uses nested blocks to help you understand the scope rules. Give the output that this code fragment would produce if embedded in an otherwise complete, correct program.

```
{
    int x = 1;
    cout << x << endl;
    {
        cout << x << endl;
        int x = 2;
        cout << x << endl;
        {
            cout << x << endl;
            int x = 3;
            cout << x << endl;
        }
        cout << x << endl;
    }
    cout << x << endl;
}
```

# 3.3 MORE ABOUT C++ LOOP STATEMENTS

> It is not true that life is one damn thing after another—
> It’s one damn thing over and over.
> 
> EDNA ST. VINCENT MILLAY, Letter to Arthur Darison Ficke, October 24, 1930

A loop is any program construction that repeats a statement or sequence of statements a number of times. The simple while loops and do-while loops that we have already seen are examples of loops. The statement (or group of statements) to be repeated in a loop is called the body of the loop, and each repetition of the loop body is called an iteration of the loop. The two main design questions when constructing loops are: What should the loop body be? How many times should the loop body be iterated?

# The while Statements Reviewed

The syntax for the while statement and its variant, the do-while statement, is reviewed in Display 3.9. The important difference between the two types of