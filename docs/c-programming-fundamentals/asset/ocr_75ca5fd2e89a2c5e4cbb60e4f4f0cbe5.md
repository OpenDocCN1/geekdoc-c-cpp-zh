21
Enter your Undergraduate Year
2024
Sorry, you cannot appear

# Code Debriefing

+   - This code shows that the display function of our class exists in multiple forms.
+   - Static binding is implemented here using function overloading.
+   - The functions all have the same name, but different signatures. That is, they have different combinations and numbers of parameters.
+   - While calling the display function, keep in mind which signature calls which function.
+   - Here, the compiler gets to know about the code attached to the function call only at compile time.

# Code: Dynamic binding

```
#include <iostream>
using namespace std;
class person
{
    public:
    virtual void display()
    {
        cout<<"Enter your age"<<endl;
    }
};
class student : public person
{
    public :
    void display()//overridden
    {
        cout<<"Enter your Under Graduaate Year"<<endl;
    }
};

int main()
{
    person e;
```