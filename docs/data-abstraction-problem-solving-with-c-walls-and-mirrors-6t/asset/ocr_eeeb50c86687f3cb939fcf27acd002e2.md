you terminate the loop and report that the string is not balanced. To verify condition 2, you check that the stack is empty when the end of the string is reached.

Thus, the pseudocode solution to check for balanced braces in aString becomes

```
// Checks the string aString to verify that braces match.
// Returns true if aString contains matching braces, false otherwise.
checkBraces(aString: string): boolean
    aStack = a new empty stack
    balancedSoFar = true
    i = 0
    while (balancedSoFar and i < length of aString)
    {
        ch = character at position i in aString
        i++
        // Push an open brace
        if (ch is a '{')
            aStack.push('{')
        // Close brace
        else if (ch is a '}')
        {
            if (!aStack.isEmpty())
                aStack.pop() // Pop a matching open brace
            else
                balancedSoFar = false
        } // Ignore all characters other than braces
    }
    if (balancedSoFar and aStack.isEmpty())
        aString has balanced braces
    else
        aString does not have balanced braces
```

A detailed pseudocode solution to check a string for balanced braces

Figure 6-3 shows the stacks that result when this algorithm is applied to several simple examples.

# FIGURE 6-3 Traces of the algorithm that checks for balanced braces

| Input string | Stack as algorithm executes | |
| :--- | :--- | :--- |
| | 1. | 2. | 3. | 4. | |
| {a{b}c} | { | { { | { { { | { { { { | 1. push (
2. push (
3. push (
4. pop
Stack empty => balanced |
| {a{bc} | { | { { | { { { | | 1. push (
2. push (
3. pop
Stack not empty => not balanced |
| {ab}c} | { | { | | | 1. push (
2. pop
Stack empty when next "}" encountered => not balanced |