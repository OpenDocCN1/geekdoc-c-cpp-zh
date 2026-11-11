Let’s now learn how to add an object and a built-in data type.

# Using Type Operator for Type Conversion

In C++, you can also overload a datatype, such as int, float. The overloading of a data type is also called as overloading of a type operator. The following syntax is used to overload a type operator:

```
```cpp
className::operator typename ()
{
...
...
}
```
```

The return type of the operator function that overloads a type operator is same as the type operator. Listing 51 shows an example of type conversion using type operator (you can find this example in the TypeConversion.cpp file on the CD in the code\chapter6 folder):

# Listing 51: Overloading of a Type Operator

```
```cpp
#include<iostream.h>

class TypeConverter
{
    int num,
    total,percentage;
    public:
    TypeConverter(int,int);
    operator int()
    {
        percentage=num*100/total;
        return percentage;
    }
};

TypeConverter::TypeConverter(int n,int t)
{
    num=n;
    total=t;
    percentage=0;
}
int main()
{
    TypeConverter tcv(45,500);
    cout<<"The result of the 'operator int()' type operator is : ";
    cout<<tcv.operator int()<<"\n";
    return 0;
}
```
```