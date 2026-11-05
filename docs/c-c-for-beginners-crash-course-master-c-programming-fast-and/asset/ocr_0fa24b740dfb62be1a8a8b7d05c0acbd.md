# # Chapter 8 Classes and Methods in C#

# ## 8.1 Class declaration

In C# classes are the primary building blocks of the language. It provides predefined set of variables and methods. Objects are defined as an instance of a class, therefore the methods inside the class determine what can be executed on the object.

# ### Class Definition

A class definition starts with keyword **class** followed by the actual class name. The class variables and methods are all enclosed in between the curly brackets; this area is also called the class body.

# ### Syntax:

```
```text
<access specifier>class class_name
{
                //member variables
                <access specifier> <data type> variable1;
                <access specifier> <data type> variable2;
                ……
                <access specifier><data type> variableN;
                //member methods
                <access specifier><return type>method1(parameter_list)
                {
                                //method body
                }
                <access specifier><return type>method2(parameter_list)
                {
                                //method body
                }
                ….. 
                <access specifier><return type>methodN(parameter_list)
                {
                                //method body
                }
```

```