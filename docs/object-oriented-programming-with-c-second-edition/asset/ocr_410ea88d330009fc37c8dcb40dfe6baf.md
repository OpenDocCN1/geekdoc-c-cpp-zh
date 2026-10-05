;
/*End of nestPrivate.h*/

In Listing 2.49, class B is defined in the public section of class A.

# **Listing 2.49** A public nested class

```
/*Beginning of nestPublic.h*/
class A
{
    public:
        class B
        {
            /*
            definition of class B
            */
        };
        /*
        definition of class A
        */
};\n/*End of nestPublic.h*/
```

A nested class is created if it does not have any value a name collision. In Listings 2.48 and 2.49, even if there is a class B defined as a global class, its name as a nested class, its name will not clash with the nested class B.
The size of objects of an enclosing class is not affected by the presence of nested classes.
See Listing 2.50.

# **Listing 2.50** Size of objects of the enclosing class

```
/*Beginning of nestSize.cpp*/
#include<iostream>
class A
{
    int x;
    public:
        class B
        {
            int y;
        };
    };
void main()
{
    cout<<sizeof(int)<<endl;
    cout<<sizeof(A)<<endl;
}
/*End of nestSize.cpp*/
```

# **Output**
4
4

How are the member functions of a nested class defined? Member functions of a nested class can be defined outside the definition of the enclosing class. This is done by prefixing