# 276 7 Inheritance and Derivation

```
);
class D1: public B1    //define publicly derived class D1
{
public:
    void display(cout<<"D1::display()"<<endl);
    //public member function
}
void fun(B0 *ptr)        //ordinary function
{
    //the argument is a pointer of the base class
    ptr->display();      //object pointer -> member
}
```

```
int main()
{
    B0 b0;              //declare an object of class B0
    B1 b1;               //declare an object of class B1
    D1 d1;               //declare an object of class D0
    B0 *p;               //declare an pointer of class B0
    p=&b0;              //pointer of B0 points to
    fun(p);
    p=&b1;              //pointer of B0 points to B1 object
    fun(p);
    p=&d1;              //pointer of B0 points to D1 object
    fun(p);
}
```

In the above example, by using the terms "object name. member name" or "object pointer->member name", we can access newly added homonym members in the derived classes. According to the type compatible rule, we can assign the address of an object of the derived class to a pointer of the base class BO, while only the members inherited from the base class can be accessed through this.

In the program, we declare an ordinary function fun with a pointer of base class BO as its formal argument. Based on the type compatible rule that the address of an object of the publicly derived class can be assigned to a pointer of the base class, function fun can operate uniformly on the objects of this class family. In the execution of the program, the addresses of the base class, the derived class B1, and D1, are respectively assigned to the base pointer p. However, through pointer p we can only access members inherited from the base class. That is to say, although the pointer points to an object of the derived class D1, during the execution of the function fun we can only access the member function display inherited from the base class BO instead of the homonym function declared in class D1 through the pointer p. Thus, the three calls of function fun in main() have the same