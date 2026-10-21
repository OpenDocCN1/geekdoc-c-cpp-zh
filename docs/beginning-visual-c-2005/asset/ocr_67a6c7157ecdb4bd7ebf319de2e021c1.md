Note how you only put the parameter name T along with the class name before the scope resolution operator. This is necessary — the parameters are fundamental to the identification of the class to which a function, produced from the template, belongs. The type is CSamples<T> with whatever type you assign to T when you create an instance of the class template. Your type is plugged into the class template to generate the class definition and into the function template to generate the definition for the Max() function for the class. Each class produced from the class template needs to have its own definition for the function Max().

Defining a constructor or a destructor outside of the class template definition is similar. You could write the definition of the constructor that accepts an array of samples as:

```
template<class T>
CSamples<T>::CSamples(T values[], int count)
{
    m_Free = count < 100? count:100;      // Don't exceed the array

    for(int i = 0; i < m_Free; i++)
        m_Values[i] = values[i];          // Store count number of samples
}
```

The class to which the constructor belongs is specified in the template in the same way as for an ordinary member function. Note that the constructor name doesn’t require the parameter specification(it is just CSamples, but it needs to be qualified by the class template type CSamples<T>. You only use the parameter with the class template name preceding the scope resolution operator.

# Creating Objects from a Class Template

When you use a function defined by a function template, the compiler is able to generate the function from the types of the arguments used. The type parameter for the function template is implicitly defined by the specific use of a particular function. Class templates are a little different. To create an object based on a class template, you must always specify the type parameter following the class name in the declaration.

For example, to declare a CSamples<> object to handle samples of type double, you could write the declaration as:

```
CSamples<double> myData(10.0);
```

This defines an object of type CSamples<double> that can store samples of type double, and the object is created with one sample stored with the value 10.0.

# Try It Out   Class Templating

You could create an object from the CSamples<> template that stores CBox objects. This works because the CBox class implements the operator>() function to overload the greater-than operator. You could exercise the class template with the main() function in the following listing:

```
// Ex8_07.cpp
// Using a class template
#include <iostream>
```