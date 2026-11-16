```
fout.open("A.doc", ios::out);

if(!fout)
{
    cout<<"Can't open";
    return -1;
}

fout<<"Hello World\fHello World";

fout.close();
}
```

Here, a file A.doc will be created and written. When you will open A.doc, you will see Hello World written in two different pages. This confirms the fact that the character \f separates the forms.

![](bbox=[0.12, 0.44, 0.93, 0.62])

# \n Newline

This character is for line feed i.e. whatever we write after this character is written in new line. Consider the following program:

```
#include<iostream>

using namespace std;

int main()
{
    cout<<"Hello\nWorld";
}
```