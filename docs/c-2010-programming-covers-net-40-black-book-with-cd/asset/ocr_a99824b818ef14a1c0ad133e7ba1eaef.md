```
MyFirstInterface I1 = (MyFirstInterface)ABC;
MySecondInterface I2 = (MySecondInterface)ABC;
I1.MyFirstMethod();
I2.MySecondMethod();
}
public void MyFirstMethod()
{
    Console.WriteLine("Call  MyFirstMethod() ");
}
public void MySecondMethod()
{
    Console.WriteLine("Call  MySecondMethod() ");
}
```

In the preceding code snippet, the ImplementInterface class implements the MyFirstInterface and MySecondInterface interfaces. The MyFirstInterface interface contains a method MyFirstMethod() and the MySecondInterface interface contains a method MySecondMethod() both of which do not return any value. As seen in the preceding code snippet, we write the body of methods in the class that implements the interfaces.

# Interfaces and Inheritance

When an interface is implemented by a base class, then the derived class of the base class automatically inherits method of the interface. You can initialize an object of the interface by type casting the object of the derived class with the interface itself. Consider the following code snippet to understand the concept of interface and inheritance more clearly:

```
interface MyInterface
{
void ShowData();
}
class MyBaseClass:MyInterface //Implements MyInterface
{
public void ShowData()
{
//Method Body
}
}
class MyDerivedClass:MyBaseClass //Inherits MyBaseClass
{
public new void ShowData()
{
//Method Body
}
}
class MainClass
{
...
MyDerivedClass dc=new MyDerivedClass()
dc.ShowData();
MyInterface inter=(MyInterface) dc;
inter.ShowData();
}
```

In the preceding code snippet, an interface, MyInterface, is declared containing the ShowData() method. A base class, MyBaseClass, implements the MyInterface interface. Next, a derived class, MyDerivedClass, inherits the MyBaseClass class. Now, in the MainClass class an instance, dc, of the MyDerivedClass class is declared and initialized. Finally, the dc object is type casted to the inter object of the MyInterface interface and used to call the ShowData() method.

Let’s now move on to the Immediate Solutions section of this chapter.