# 52 2 Elementary C++ Programming

Attention: statement 1, 2, 3, and 4 can be a compound statement; the if of each hierarchy has to match with an else. If you want to omit one else, you must use {} to enclose the statement if that hierarchy to the correct hierarchy relation.

**Example 2.3:** Compare two numbers.

Analysis: compare two numbers x and y; there are three resulting possibilities: x=y, x>y and x<y. Therefore, we need a multiple selection structure. We choose the nested else statement here.

Source code:

```
cpp
//2_3.cpp
#include<iostream>
using namespace std;
int main()
{
    int x,y;
    cout<<"Enter x and y:";
    cin>>x>>y;
    if (x!=y)
        cout<<"x>y"<<endl;
    else
        cout<<"x<y"<<endl;
n}
```

Result 1:

| Enter x and y:5 8 |
| x<y |

Result 2:

| Enter x and y:8 8 |
| x=y |

Result 3:

| Enter x and y:12 8 |
| x>y |

# **2. if...else Statement**

If all the nested if statements are in a branch else, we can use the statement if...else if. The syntax form is: