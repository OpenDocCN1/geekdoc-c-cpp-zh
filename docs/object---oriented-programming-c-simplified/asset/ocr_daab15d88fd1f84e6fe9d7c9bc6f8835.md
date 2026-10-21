# 9.8 CONTAINERSHIP

We can create object of one class into another and that object will be a member of the class. This type of relationship between classes is known as **has_a** relationship as one class contains object of another class. The inheritance which we have seen till now is considered **kind_of** or **is_a** relationship.

```
/*PROG 9.38 DEMO OF CONTAINERSHIP VER 1*/

#include <iostream.h>
#include <conio.h>
class first
{
    public :
        void showf( )
        {
            cout<<"Hello from first"<<endl;
        }
};
class second
{
    first f;
    public :
    second( )
    {
        f.showf( );
    }
};
void main( )
{
    clrscr( );
    second s;
    getch( );
}

OUTPUT :
Hello from first
```

**EXPLANATION :** In the class second we have an object of class first. This is another type of inheritance we are witnessing. This type of inheritance is known as has_a relationship as we say that class second has an object of class first as it s member. Form this object f we call the function of class first.