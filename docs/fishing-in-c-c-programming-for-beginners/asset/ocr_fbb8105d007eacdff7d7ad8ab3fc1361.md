```
}
Output
Hello world   Black
```

This is generally used to create a menu bar on output screen. E.g. Consider the following program:

```
#include<iostream>
using namespace std;
int main()
{
    cout<<"1.File\t2.Edit\t3.View\t4.Search\t5.Exit";
}
```

```
Output
1.File   2.Edit   3.View   4.Search   5.Exit
```

# Various uses of backslash

Suppose we are illustrating \b to someone, and we have to display \b and not its effect. Then, you may think that cout<<"\b"; will display \b, then you will suddenly realize, no it will instead try to move the cursor one step backward. Then, how to print \b. The solution is to use double backslash. E.g. Consider the following program

```
#include<iostream>
using namespace std;
int main()
{
    cout<<"\\b";
    cout<<"\\n";
    cout<<"\\n";
    cout<<"\\n";
    cout<<"\\"";
```