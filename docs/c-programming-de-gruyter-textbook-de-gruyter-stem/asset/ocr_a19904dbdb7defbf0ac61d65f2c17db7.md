Parameters should be separated by commas if there is more than one parameter in the list. Moreover, member functions of a template class have to be function templates.

The compiler does not generate codes immediately when it sees declarations of class templates, which only declare a series of classes. The compiler generates codes on demand when it figures out a template is referenced.

The form for using a template class is as follows:

```
Template<ParameterList> Object1, ...Object n;
```

Fig 9.3 demonstrates how to represent template classes in a UML graph, in which T is a formal parameter indicating the type information in the class.

The compiler generates concrete classes by binding actual types to formal parameters, which are often called "instantiation". The UML represents the dependency of instantiation by the <<bind>> operation. There are two forms of showing binding elements, as in Figure 9.4:

Each parameter in the ParameterList corresponds to the parameter in the class template declaration. The compiler generates a class based on the constants and the types of parameter, then instantiates the class to generate an instance. That is say, the compiler instantiates the class template to generate a concrete class and instantiates the class to produce an object.

![](bbox=[0.18, 0.483, 0.88, 0.631])

Fig. 9.3: Parameterized class with explicit attributes and methods.

![](bbox=[0.18, 0.643, 0.84, 0.856])

Parameterized class A Use parameter to bind elements Use <<bind>> to bind elements-

Fig. 9.4: Forms of binding elements in parameterized class.