CBox Multiply: n odd
: 3*aBox

![](bbox=[0.47, 0.095, 0.67, 0.26])

![](bbox=[0.21, 0.285, 0.41, 0.43])

CBox Multiply: n even
: 6*aBox

![](bbox=[0.57, 0.46, 0.77, 0.69])

# Figure 8-6

Of course, you don’t need to check which is the larger of the length and width for the new object because the constructor will sort it out automatically. You can write the version of the operator*() function as a member function with the left operand as a CBox object:

```
// CBox multiply operator this*n
CBox operator*(int n) const
{
    if(n % 2)
        return CBox(m_Length, m_Width, n*m_Height);        // n odd
```