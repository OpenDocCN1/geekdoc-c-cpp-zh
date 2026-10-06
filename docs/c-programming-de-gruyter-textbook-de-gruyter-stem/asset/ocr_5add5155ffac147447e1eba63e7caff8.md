# 5.3 Static Members of Class 167

although this static data member is private, it can be initialized directly. Except for this special occasion, in other places, such as in the main function, direct access is allowed. The value of count is calculated in the constructor; where object A is created, the constructor with default parameters is called; when object B is created, the copy constructor is called. These two constructors access the same static member count. Also, the output of calling function GetC object A and B respectively is the values of the same count at different times. In this way, we can achieve data sharing between A and B directly.

The result of the program:

```
Point A,4,5 Object id=1
Point B,4,5 Object id=2
```

Furthermore, we usually access static data members through noninline functions, because the compiler will make sure it has initialized the static data members before calling any noninline functions. However, when using inline functions to call static members from another compiling unit, it is possible that the static member has not initialized yet; therefore this kind of calling is unsafe.

# 5.3.2 Static Function Member

In Example 5.3, function GetC() is devoted to output static member count. We can only output count by calling function GetC() through one object of class Point. Before declaring all the objects, the value of count is its initial value 0. How can we output this initial value? It is obvious that we cannot call GetC() through an object since there has no object declared yet. Because count belongs to the whole class instead of any object, we hope to access count without going objects. Now us try to write the main function in Example 5.3 as follows:

```
int main()
{
    Point::GetC(); //call the function directly through class name
    //to output the initial value of the number of
    //objects

    Point A(4,5);
    cout<<"Point A","<<A.GetX()","<<A.GetY()"";
    A.GetC();
    Point B(A);
    cout<<"Point B","<<B.GetX()","<<B.GetY()"";
    B.GetC();
}
```