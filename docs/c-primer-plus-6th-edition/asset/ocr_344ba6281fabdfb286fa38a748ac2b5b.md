```
double x;
cout << "Enter value: ";
while (! (cin >> x) )
{
    cout << "Bad input. Please enter a number: ";
    cin.clear();
    while (cin.get() != '\n')
        continue;
}
cout << "Value = " << x << endl;
return 0;
}
```

5. You could have separate static function definitions in each file. Or each file could define the appropriate average() function in an unnamed namespace.

6. 10
4
0
Other: 10, 1
another(): 10, -4

7. 1
4, 1, 2
2
2
4, 1, 2
2

# Answers to Chapter Review for Chapter 10

+   1. A class is a definition of a user-defined type. A class declaration specifies how data is to be stored, and it specifies the methods (class member functions) that can be used to access and manipulate that data.

+   2. A class represents the operations you can perform on a class object with a public interface of class methods; this is abstraction. The class can use private visibility (the default) for data members, meaning that the data can be accessed only through the member functions; this is data hiding. Details of the implementation, such as data representation and method code, are hidden; this is encapsulation.

+   3. A class defines a type, including how it can be used. An object is a variable or another data object, such as that produced by new, which is created and used according to the class definition. The relationship between a class and an object is the same as that between a standard type and a variable of that type.