# 10.6 Common Programming Errors

The common programming errors associated with constructing classes are as follows:

+   1. Failing to terminate the class declaration section with a semicolon.
+   2. Including a return type with the constructor's prototype or failing to include a return type with the other methods' prototypes.
+   3. Using the same name for a data member as for a member method.
+   4. Defining more than one default constructor for a class.
+   5. Forgetting to include the class name and scope operator, ::, in the header of all member methods defined in the class implementation section.
+   6. Using the static keyword when defining a static data member or member method. It should be used only in the class declaration section.
+   7. Using the friend keyword when defining a friend function. It should be used only in the class declaration section.
+   8. Failing to instantiate static data members before creating class objects that must access these data members.

# 10.7 Chapter Summary

+   1. A class is a programmer-defined data type. Objects of a class can be defined and have the same relationship to their class as variables do to C++'s built-in data types.
+   2. A class definition consists of declaration and implementation sections. The most common form of a class definition is as follows:

```
// class declaration section
class name
{
    private:
        // a list of variable declarations;
    public:
        // a list of method prototypes;
};
// class implementation section
// class method definitions
```

The variables and methods declared in the class declaration section are collectively called class members. The variables are referred to as class data members, and the methods are referred to as class member methods. The keywords private and public are access specifiers. After an access specifier is listed, it remains in force until another access specifier is given. The private keyword specifies that class members following it are private to the class and can be accessed only by member methods. The public keyword specifies that the class members following it can be accessed from outside the class. Generally, all data members should be specified as private and all member methods as public.