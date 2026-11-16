However, following names are valid

```
int num1=5; int _num=5; int num_a8=9;
```

# Variable constraint: Limitations of variables

Now, consider a question, Can a variable store a number to any number of digits after the decimal point if it lies within its range? Let us see:

```
#include<iostream>
using namespace std;
int main()
{
    float a=2.523456789;
    float b=2123456.789;
    cout<<a;
    cout<<endl<<b<<endl;
    cout<<a*b<<endl;
    cout<<2.523456789*2123456.789<<endl;
    cout<<(a*b-5358450);
}
```

Output

```
2.52346
2.12346e+006
5.35845e+006
5.35845e+006
1.5
```

Well, if you are not accustomed to e+ symbol then you will be pleased to know that this is the way to represent the scientific notation into computer. E.g. 3e-004 means 3*10^4.

The product 2.523456789*2123456.789=5358451.45. While it displays 5358450 but this does not mean it has stored this result as our last line of output shows, where we told the