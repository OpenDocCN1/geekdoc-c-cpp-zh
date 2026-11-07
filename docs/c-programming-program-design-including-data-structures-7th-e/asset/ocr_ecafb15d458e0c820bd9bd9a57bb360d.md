```
```cpp
private:
    personType name;
    dateType bDay;
    int personID;
};
```
```

Figure 11-8 shows the UML class diagram of the class `personalInfo` and composition (aggregation).

![](bbox=[0.199, 0.262, 0.897, 0.488])

**FIGURE 11-8** UML class diagram of the class `personalInfo` and composition (aggregation)

Before we give the definition of the member functions of the class `personalInfo`, let us discuss how the constructors of the objects `bDay` and `name` are invoked.

Recall that a class constructor is automatically executed when a class object enters its scope. Suppose that we have the following statement:

```
```cpp
personalInfo student;
```
```

When the object `student` enters its scope, the objects `bDay` and `name`, which are members of `student`, also enter their scopes. As a result, one of their constructors is executed. We, therefore, need to know how to pass arguments to the constructors of the member objects (that is, `bDay` and `name`), which occurs when we give the definitions of the constructors of the class. Recall that constructors do not have a type and so cannot be called like other functions. The arguments to the constructor of a member object (such as `bDay`) are specified in the heading part of the definition of the constructor of the class. Furthermore, member objects of a class are constructed (that is, initialized) in the order they are declared (not in the order they are listed in the constructor’s member initialization list) and before the containing class objects are constructed. Another way to think of this is that all of the components that make up the instance of `personalInfo` must be built before the instance itself can be built. Thus, in our case, the object name is initialized first because it is the first member listed (in the private section of the class `personalInfo`), then `bDay` (the second member listed), and finally `student` (the instance of `personalInfo` we are declaring).

The following statements illustrate how to pass arguments to the constructors of the member objects `name` and `bDay`: