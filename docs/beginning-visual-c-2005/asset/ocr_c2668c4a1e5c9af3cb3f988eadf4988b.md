```
else
    return CBox(m_Length, 2.0*m_Width, (n/2)*m_Height);    // n even
}
```

Here, you use the % operator to determine whether n is even or odd. If n is odd, the value of n % 2 is 1 and the if statement is true. If it’s even, n % 2 is 0 and the statement is false.

You can now use the function you have just written in the implementation of the version with the left operand as an integer. You can write this as an ordinary non-member function:

```
// CBox multiply operator n*aBox
CBox operator*(int n, const CBox& aBox)
{
    return aBox*n;
}
```

This version of the multiply operation simply reverses the order of the operands so as to use the previous version of the function directly. That completes the set of arithmetic operators for CBox objects that you defined. We can finally look at the two analytical operator functions, operator/() and operator%().

# Analyzing CBox Objects

As I have said, the division operation determines how many CBox objects are identical to that specified by the right operand can be contained in the CBox object specified by the left operand. To keep it relatively simple, assume that all the CBox objects are packed the right way up, that is, with the height dimensions vertical. Also assume that they are all packed the same way round, so that their length dimensions are aligned. Without these assumptions, it can get rather complicated.

The problem then amounts to determining how many of the right-operand objects can be placed in a single layer, and then deciding how many layers we can get inside the left-operand CBox.

You can code this as a member function like this:

```
int operator/(const CBox& aBox)
{
    int tc1 = 0;        // Temporary for number in horizontal plane this way
    int tc2 = 0;        // Temporary for number in a plane that way

    tc1 = static_cast<int>((m_Length / aBox.m_Length))* static_cast<int>((m_Width / aBox.m_Width));    // to fit this way
    tc2 = static_cast<int>((m_Length / aBox.m_Width))* static_cast<int>((m_Width / aBox.m_Length));    // and that way

    //Return best fit
    return static_cast<int>((m_Height/aBox.m_Height)*(tc1>tc2 ? tc1 : tc2));
}
```

This function first determines how many of the right-operand CBox objects can fit in a layer with their lengths aligned with the length dimension of the left-operand CBox. This is stored in tc1. You then calculate how many can fit in a layer with the lengths of the right-operand CBoxes lying in the width direction of the left-operand CBox. Finally you multiply the larger of tc1 and tc2 by the number of layers you can pack in, and return that value. This process is illustrated in Figure 8-7.