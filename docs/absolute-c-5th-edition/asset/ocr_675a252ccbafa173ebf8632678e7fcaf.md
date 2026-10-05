# Algorithm Abstraction

As we saw in our discussion of the swapValues function, there is a very general algorithm for interchanging the value of two variables that applies to variables of any type. Using a function template, we were able to express this more general algorithm in C++. This is a very simple example of algorithm abstraction. When we are using algorithm abstraction, we mean that we are expressing our algorithms in a very general way that we can ignore incidental detail and concentrate on the substantive part of the algorithm. Function templates are one feature of C++ that supports algorithm abstraction.

![](bbox=[0.125, 0.287, 0.191, 0.335])

# TIP: How to Define Templates

When we defined the function templates in Display 16.1, we started with a function that sorts an array of elements of type int. We then created a template by replacing the base type of the array with the parameter T. This is a general strategy for writing templates. If you want to write a function template, first write a version that is not a template at all is just an ordinary function. Completely debugging the ordinary function, and finally convert the ordinary function to a template by replacing some type name with a type parameter. There are two advantages to dealing with a much more concrete case, which makes the problem easier to visualize. Second, you have fewer details to check at each stage; when worrying about the algorithm itself, you need not concern yourself with template syntax rules.

# Function Template

The function and the function declaration for a function template are each prefaced with the following:

```
template<class Type_Parameter>
```

The function declaration (if used) and definition are then the same as any ordinary function declaration and definition, except that the Type_Parameter can be used in place of a type.


For example, this function template might be as follows:

```
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3);
```

The definition for this function template might be as follows:

```
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3)
{
    cout << stuff1 << endl;
    cout << stuff2 << endl;
    cout << stuff3 << endl;
}
```