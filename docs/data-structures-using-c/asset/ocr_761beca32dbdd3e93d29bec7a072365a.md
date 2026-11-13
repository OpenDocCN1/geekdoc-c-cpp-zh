```
PROGRAM CODE 3.4
Stack :: m_push(int i, char x)
{
    // push x to the i'th stack
    if(t[i] == s(i + 1))
        Stack_full(i);
    else
    {
        t[i] = t[i] + 1;
        A[t[i]] = x;
    }
}

char Stack::m_pop(int i)
{
    // pop topmost element of stack i
    if(t[i] == s(i))
        Stack_empty(i);
    else
    {
        t[i] = t[i] - 1;
        return(A[t[i] + 1]);
    }
}
```

Stack_full() and Stack_empty() are the functions to be written depending on the strategy followed in each case. For example, if we permit the addition of elements to stacks as long as there is some free space in array A, the following steps may be one of the solutions to this:

+   1. Determine the last i < j <= m, such that there is a free space between the stacks j and j + 1, that is, t[j] <= s[j + 1]. If there is such an A[j], we can move the stacks i + 1, i + 2, ..., j one position to the right (treating A[n] as the rightmost) and can create a space between the stacks i and i + 1.
+   
+   2. If there is no j in step 1, then check the left side of stack i. Find the largest j such that 1 <= j <= i and there is space between the stacks j and j + 1, that is, t[j] < s[j + 1]. If there is such a j, then move the stacks j + 1, j + 2, ..., i by one space left, creating a free space between the stacks i and i + 1.
+   
+   3. If there is no such j satisfying the conditions of either steps 1 or 2, then all the n spaces of A are utilized, and there is no free space.