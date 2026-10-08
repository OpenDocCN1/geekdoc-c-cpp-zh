reference to a method. The variable that uses this keyword must not be initialized before the method call to ensure that the programmer understands its intended effects. Using out requires the developer to specify the keyword even in calling code so to ensure that it is easily visible to developers reading the code that the variable will have its value changed elsewhere. This is useful when analyzing the program flow.

+   46. Override – it is used in declaring an overridden function, which extends a base class function of the name.

+   47. Params – it is used to describe when groupings of parameters are passed to a method. The number of methods is not important as they can vary. The params keyword must be the last variable in a method signature as it is not important, so that the compiler can deal with the parameters which have been defined.

+   48. Private – it is used in field, property, and method declarations to make the field, property, or method private to its enclosing class. This means that it is not visible outside of its class.

+   49. Public – it is used in field, property, and method declarations to make the field, property, or method public to its enclosing class. This means that it is visible from any class.

+   50. Protected – it is used in field, property, and method declarations to make the field, property, or method protected to its enclosing class. This means that it is not visible outside of its class.

+   51. Readonly- it is strongly related to const keyword, with the exception of allowing a variable with its modifier to be initialized in a constructor, along with being associated with a class instance rather than the class itself.

+   52. Ref – it explicitly specifies that a variable should be passed by reference rather than by value.

+   53. Return – this keyword is used to return execution from a method or from a property accessor. In case a method or property accessor has a return type,