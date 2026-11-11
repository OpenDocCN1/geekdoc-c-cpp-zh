```
```cpp
if (b==0)
{
    throw b;
}
c = a/b;
cout<<"Result of division is "<<c<<endl;
printData(p);
}
catch(...)
{
cout<<"Some exception has occured"<<endl;
}
d = a+b;
cout<<"Result of addition is "<<d<<endl;
}

Output
Enter two numbers
10 2
Result of division is 5
Some exception has occured
Result of addition is 12
```
```

# 17.5  Order of writing Catch Blocks

If your program has both specialized and generic catch blocks, all the specialized catch blocks must always appear before the generic catch block as shown in Figure 17.2. This is because the generic catch block has a potential to catch all the types of exceptions, and if it is written before the specialized one’s, the specialized catch blocks will never get executed as all the special exceptions will also be caught by the generalized catch block itself.

![](bbox=[0.203, 0.622, 0.7, 0.906])

```
```cpp
try
{
    /*Code that may throw an exception*/
}
catch(int a)
{
    /*Special catch block to handle int type objects*/
}
catch(char a)
{
    /*Special catch block to handle char type objects*/
}
catch(float a)
{
    /*Special catch block to handle float type objects*/
}
catch(...)
{
    /*Generic catch block*/
}
```
```

Figure 17.2: Order of writing catch blocks