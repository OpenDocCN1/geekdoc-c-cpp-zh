rewritten code, it’s now clear that some of the 1s and 0s in the original Visual Basic example weren’t being used as boolean flags. The If reportSelected = 1 line was not a boolean test at all; it tested whether the first report had been selected.

This approach tells the reader that you’re making a boolean test. It’s also harder to write true when you mean false than it is to write 1 when you mean 0, and you avoid spreading the magic numbers 0 and 1 throughout your code. Here are some tips on defining true and false in boolean tests:

# Compare boolean values to true and false implicitly

You can write clearer tests by treating the expressions as boolean expressions. For example, write

```
while ( not done ) ...
while ( a > b ) ...
```

rather than

```
while ( done = false ) ...
while ( (a > b) = true ) ...
```

Using implicit comparisons reduces the number of terms that someone reading your code has to keep in mind, and the resulting expressions read more like conversational English. The previous example could be rewritten with even better style like this:

# Better Visual Basic Examples of Testing for True and False Implicitly

```
Dim printerError As Boolean
Dim reportSelected As ReportType
Dim summarySelected As Boolean
...
If ( Not printerError ) Then InitializePrinter()
If ( printerError ) Then NotifyUserOfError()

If ( reportSelected = ReportType_First ) Then PrintReport()
If ( summarySelected ) Then PrintSummary()

If ( Not printerError ) Then CleanupPrinter()
```

> Cross-Reference For details, see Section 12.5, "Boolean Variables."

If your language doesn’t support boolean variables and you have to emulate them, you might not be able to use this technique because emulations of true and false can’t always be tested with statements like while ( not done ).

# Making Complicated Expressions Simple

You can take several steps to simplify complicated expressions:

# Break complicated tests into partial tests with new boolean variables

Rather than creating a monstrous test with half a dozen terms, assign intermediate values to terms that allow you to perform a simpler test.