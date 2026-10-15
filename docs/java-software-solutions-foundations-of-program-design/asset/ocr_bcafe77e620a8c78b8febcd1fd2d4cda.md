# SELF-REVIEW QUESTIONS *(see answers in Appendix N)*

**SR 7.18** What is method decomposition?

**SR 7.19** Answer the following questions about the `PigLatinTranslator` class.

+   a. No constructor is defined. Why not?
+   
+   b. Some of the defined methods are private. Why?
+   
+   c. A `Scanner` object is declared in the `translate` method. What is it used to scan?

**SR 7.20** Identify the resultant sequence of calls/returns of `PigLatinTranslator` support methods when `translate` is invoked with the following actual parameters.

+   a. `"animal"`
+   
+   b. `"hello"`
+   
+   c. `"We are the champions"`

**SR 7.21** How are objects passed as parameters?

# 7.8 Method Overloading

As we’ve discussed, when a method is invoked, the flow of control transfers to the code that defines the method. After the method has been executed, control returns to the location of the call, and processing continues.

Often the method name is sufficient to indicate which method is being called by a specific invocation. But in Java, as in other object-oriented languages, you can use the same method name with different parameter lists for multiple methods. This technique is called *method overloading*. It is useful when you need to perform similar methods on different types of data.

The compiler must still be able to associate each invocation to a specific method declaration. If the method name for two or more methods is the same, additional information is used to uniquely identify the version that is being invoked. In Java, a method name can be used for multiple methods as long as the number of parameters, the types of those parameters, and/or the order of the types of parameters is distinct.

For example, we could declare a method called `sum` as follows:

```
public int sum (int num1, int num2)
{
    return num1 + num2;
}
```

> **KEY CONCEPT**
> 
> The versions of an overloaded method are distinguished by the number, type, and order of their parameters.