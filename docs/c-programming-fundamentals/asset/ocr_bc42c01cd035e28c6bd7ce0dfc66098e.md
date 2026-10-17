The following examples showcase how functions in C++ are overloaded and overridden.

# Code: Working with Overloaded Functions

```
#include <iostream>
using namespace std;
void display(int i)
{
    cout << " Integer  is " << i << endl;
}
void diaplay(double f)
{
    cout << "Float is " << f << endl;
}
void display(char const *c)
{
    cout << " The number of characters is  " << c << endl;
}

int main()
{
    cout<<"To show function Ooverloading "<<endl;
    display(11);
    display(11.11);
    display("Eleven");
    return 0;
}
```

# Output:

```
To show function overloading
    Integer is 11
    Integer is 11
The number of characters is Eleven
```

# Code Debriefing

+   - In this code, the display function of our class exists in multiple forms.
+   - Polymorphism is being implemented using function overloading.
+   - The functions all have the same name, but different signatures. That is, they have different combinations and numbers of parameters.
+   - While calling the display function, keep in mind which signature calls which function.