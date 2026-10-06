In fact, we don't have to specify these parameters (E and str). In many cases, it is enough to notify that the handler has an exception of a certain type. But we do need to specify parameters when accessing exception objects. Otherwise, we cannot access the object in the catch clause. For example,

```
catch( Expt )\n{
    //cannot access Expt exception object here
}
```

We can throw the exception being handled currently by a throw expression with out operands. This expression can only appear in a catch handler or the inner functions of the catch handler. The exception object being thrown again is the original exception object (not a copy). For example,

```
try
{
    throw SomeOtherException();
}catch(...) {
    //response to exceptions (maybe only a part)
    //...

    throw; //pass the exception to some other handler
}
```

# 12.4 Exception Handling of Standard Library

The C++ standard provides a standard exception structure that begins with the base exception. All exception handlings thrown by the standard library are derived from this base class. These classes are composed of derivation and inheritance relationships shown in Figure12.2. The base class provides a what() service, redefines in each derived class, and sends an error message.

The immediately derived classes runtime_error and logic_error can be derived from the base class exception directly. Each derived class can be used for deriving other classes.

When the global operator new fails, the bad_alloc exception will be thrown. During the execution, when the dynamic type operation fails, dynamic_cast will throw a bad_cast exception. In the process of type identification, if the parameter of typeid is a zero or null pointer, the bad_typeid will be thrown. When unexpected exceptions happen, the system will call the bad_exception exception