+   3. *Efficiency*: Inheritance saves a lot of time and energy in fetching data from one class to obtain the result.

+   4. *Extensibility*: Classes (as well members) are able to extend their features and functionalities through derived or child classes.

The following example of inheritance highlights its importance and ease of use.

# Code: Programming with Inheritance

```
#include <iostream>
using namespace std;
class person
{
    public:
    int age;
    void display1()
    {
        cout<<"Enter your age"<<endl;
        cin>>age;
    }
};
class student : public person
{
    public :
    int ugYear;
    void display2()
    {
        cout<<"Enter your Under Graduate passing Year"<<endl;
        cin>>ugYear;
    }
};
class exam: public student
{
    public :
    void check()
    {
        if((age>18) && (ugYear== 2021 || ugYear== 2022))
            cout<<"You Can appear for CAT 2022"<<endl;
        else
            cout<<"Sorry you Cannot appear for CAT 2022"<<endl;
    }
```