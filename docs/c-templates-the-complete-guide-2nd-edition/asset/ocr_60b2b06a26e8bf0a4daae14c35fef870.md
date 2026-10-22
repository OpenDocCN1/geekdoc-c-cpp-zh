```
void foo(Stack<int> const& s) // parameter s is int stack
{
    using IntStack = Stack<int>; // IntStack is another name for Stack<int>
    Stack<int> istack[10];       // istack is array of 10 int stacks
    IntStack istack2[10];        // istack2 is also an array of 10 int stacks (same type)
    ...
}
```