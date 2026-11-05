```
class A
{
    static void f()
    {
        int i, j;
        try
        {
            goto LABEL;
            // Neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }
        catch
        {
            // Neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }
        finally
        {
            // Neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
        }
        // i and j definitely assigned
        LABEL: ;
        // j definitely assigned
    }
}
```

# 5.3.3.16 foreach Statements

For a foreach statement stmt of the form:

foreach ( type identifier in expr ) embedded-statement

+   - The definite assignment state of v at the beginning of expr is the same as the state of v at the beginning of stmt.
+   - The definite assignment state of v on the control flow transfer to embedded-statement or to the end point of stmt is the same as the state of v at the end of expr.

# 5.3.3.17 using Statements

For a using statement stmt of the form:

using ( resource-acquisition ) embedded-statement

+   - The definite assignment state of v at the beginning of resource-acquisition is the same as the state of v at the beginning of stmt.