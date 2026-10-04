# 10.6 Chapter Summary

+   1. A class is a programmer-defined data type. Objects of a class can be defined and have the same relationship to their class as variables to C++'s built-in data types.

+   2. A class definition consists of a declaration and implementation section. The most common form of a class definition is as follows:
```
// class declaration section
class name {
  private:
    // a list of variable declarations;
  public:
    // a list of function prototypes;
  };
  // class implementation section
  // class function definitions
```

The variables and functions declared in the class declaration section are collectively called members. The variables are referred to as class data members, and the functions are referred to as class member functions. The keywords private and public are access specifiers. After an access specifier is listed, it remains in force until another access specifier is given. The private keyword specifies that class members following it are private and can be accessed only by member functions. The public keyword specifies that class members following it can be accessed from outside the class. Generally, all data members should be specified as private and all member functions as public.

+   3. Class functions listed in the declaration section can be written inline, or their definitions can be included in the class implementation section. Except for constructor and destructor functions, all class functions defined in the class implementation use this format for the header:
```
returnType className::functionName(parameter list);
```

Except for the addition of the class name and scope operator, :: which are required to identify the function within the class, this header is identical to the one used for user-written functions.

+   4. A constructor is a special function that's called each time an object is declared. It must have the same name as its class and can't have any return type. Its purpose is to initialize each declared object.

+   5. If no constructor is declared for a class, the compiler supplies a default constructor. A do-nothing function having the definition className::className(void()).

+   6. The term default constructor refers to any constructor that doesn't require arguments when it's called. The reason it doesn't require arguments is that no parameters are declared (as with the compiler-supplied default constructor) or all arguments have been given default values.

+   7. Each class can have only one default constructor. If a user-defined constructor is declared, the compiler doesn't create a default constructor.