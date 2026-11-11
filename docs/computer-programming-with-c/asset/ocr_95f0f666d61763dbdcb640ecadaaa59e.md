contains a cout statement that prints 3 tab characters, hence, each time the manipulator is invoked it will print 3 consecutive TAB spaces.

The statement

```
```cpp
cout<<"Hello"<<ETAB<<"Bye";
```
```

In the program invokes the user-defined manipulator ETAB between Hello and Bye. Hence, there will be 3 TAB spaces printed between strings Hello and Bye as shown in the output of the code.

# 15.9   Passing Arguments to the Custom Manipulator

We have created a manipulator named ETAB in the previous section. This manipulator will always print 3 tab spaces when invoked. However, the number of tabs that we would want to print on the screen might not always be fixed as 3. Programmers would like to have an ability to configure the number of TABs that are printed by this manipulator. In such a case, we will have to create a manipulator that can take a parameter, which defines the number of TABs it should print. Such manipulators are called parameterized manipulators. One of the examples of parameterized manipulator is setprecision(int precision), which takes an integer argument to set the precision for floating point numbers OR setw(int width), which takes width as a parameter to configure the output symbol spacing. Our requirement is that, we should be able to pass an integer parameter to the manipulator ETAB, to determine the actual number of TABs to be printed. For example, the statement

```
```cpp
cout<<"Hello"<<ETAB(5)<<"Bye";
```
```

should print 5 TABs between Hello and Bye since we have invoked the manipulator by passing integer constant 5.

Recall the format of creating user-defined manipulators in Figure 15.12, which supports passing custom arguments for parameterized manipulators. In this particular case, we need an additional parameter of type integer, which can give the number of TABs to be printed. Hence, we write the manipulator function, which takes an additional parameter named n

```
```cpp
ostream& NameOfTheManipulator (Arguments)
{
    /*Functionality of the manipulator*/
}
```
```

![](bbox=[0.517, 0.755, 0.879, 0.771])

```
```cpp
ostream& ETAB(ostream& p, int n)
{
        while (n>=1)
        {
                p<<"\t";
                n--;
        }
        return p;
}
```
```