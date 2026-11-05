+   - Control is transferred to the target of the continue statement.

Because a continue statement unconditionally transfers control elsewhere, the end point of a continue statement is never reachable.

# 13.10.4 The goto statement

The goto statement transfers control to a statement that is marked by a label.

```
goto_statement
  : 'goto' identifier ':'
  | 'goto' 'case' constant_expression ';'
  | 'goto' 'default' ';'
  ;
```

The target of a goto identifier statement is the labeled statement with the given label. If a label with the given name does not exist in the current function member, or if the goto statement is not within the scope of the label, a compile-time error occurs.

Note: This rule permits the use of a goto statement to transfer control out of a nested scope, but not into a nested scope. In the example

```
class Test
{
    static void Main(string[] args)
    {
        string[,] table =
        {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };
        foreach (string str in args)
        {
            int row, colm;
            for (row = 0; row <= 1; ++row)
            {
                for (colm = 0; colm <= 2; ++colm)
                {
                    if (str == table[row,colm])
                    {
                        goto done;
                    }
                }
                Console.WriteLine($"{str} not found");
                continue;
            done:
                Console.WriteLine($"Found {str} at [{row}][{colm}]");
            }
        }
    }
}
```

a goto statement is used to transfer control out of a nested scope.

end note

The target of a goto case statement is the statement list in the immediately enclosing switch statement (§13.8.3) which contains a case label with a constant pattern of the given constant value and no guard. If