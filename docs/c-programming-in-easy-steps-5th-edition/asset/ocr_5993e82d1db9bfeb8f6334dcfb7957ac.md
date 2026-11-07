+   8. After the Dog class declaration, declare a main method containing a final **return** statement

```
```cpp
int main()
{
    // Program code goes here.
    return 0 ;
}
```
```

+   9. Between the braces of the main method, declare an instance of the Dog class named “fido”

```
```cpp
Dog fido ;
```
```

+   10. Add statements calling each setter method to assign data

```
```cpp
fido.setAge( 3 );
fido.setWeight( 15 );
fido.setColor( “brown” );
```
```

+   11. Add statements calling each getter method to retrieve the assigned values

```
```cpp
cout << “Fido is a “ << fido.getColor() <<
             “dog” << endl ;
cout << “Fido is “ << fido.getAge() <<
             “ years old” << endl ;
cout << “Fido weighs “ << fido.getWeight() <<
             “ pounds” << endl ;
```
```

+   12. Now, add a call to the regular output method

```
```cpp
fido.bark() ;
```
```

+   13. Save, compile, and run the program to see the output

![](bbox=[0.3, 0.447, 0.7, 0.538])

![](bbox=[0.117, 0.548, 0.275, 0.619])

Fido

![](bbox=[0.117, 0.646, 0.208, 0.706])

This program will get modified over the next few pages as new features are incorporated.