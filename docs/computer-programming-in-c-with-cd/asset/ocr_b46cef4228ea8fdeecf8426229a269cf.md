# Creating Local Classes

A class declared within a function definition is called a local class. A local class definition can use the type names, enumerations, and static variables of the function within which the local class is defined. Listing 23 shows how to define a local class within a function definition (you can find this example in the LocalClass.cpp file on the CD in the code\chapter6 folder):

# ▶ Listing 23: Creating a Local Class

```
```cpp
#include<iostream.h>

int globalVar=100;
class A
{
    int classVar;
    public:
        static int staticVar;
        void classFun()
        {
            class B
            {
                int localClassVar;
                public:
                    void localClassFun()
                    {
                        cout<<"local class calling"<<endl;
                        localClassVar=1000;
                        cout<<"Local class variable"<<localClassVar<<endl;
                        //classVar=10;
                        //cout<<"Class variable"<<classVar<<endl;
                        cout<<"Global variable"<<globalVar<<endl;
                        cout<<"Static variable"<<A::staticVar<<endl;
                    }
            } o;
            o.localClassFun();
        }
    };
int A::staticVar=100;
void main()
{
    A oo;
    oo.classFun();
}

Output:

local class calling
```
```