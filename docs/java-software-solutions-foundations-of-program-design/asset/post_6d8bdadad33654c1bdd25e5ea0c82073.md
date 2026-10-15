
![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_365_0.png)

## FIGURE 7.4 A UML class diagram for the PigLatin program

## Method Parameters Revisited

Another important issue related to method design involves the way parameters are passed into a method. In Java, all parameters are passed by value. That is, the current value of the actual parameter (in the invocation) is copied into the formal parameter in the method header. We mentioned this issue in Chapter 4; let’s examine it now in more detail.

Essentially, parameter passing is like an assignment statement, assigning to the formal parameter a copy of the value stored in the actual parameter. This issue must be considered when making changes to a formal parameter inside a method. The formal parameter is a separate copy of the value that is passed in, so any changes made to it have no effect on the actual parameter. After control returns to the calling method, the actual parameter will have the same value as it did before the method was called.

However, when we pass an object to a method, we are actually passing a reference to that object. The value that gets copied is the address of the object. Therefore, the formal parameter and the actual parameter become aliases of each other. If we change the state of the object through the formal parameter reference inside the method, we are changing the object referenced by the actual parameter, because they refer to the same object. On the other hand, if we change the formal parameter reference itself (to make it point to a new object, for instance), we have not changed the fact that the actual parameter still refers to the original object.

> KEY CONCEPT
> When an object is passed to a method, the actual and formal parameters become aliases.

The program in Listing 7.15 illustrates the nuances of parameter passing. Carefully trace the processing of this program and note the values that are output. The ParameterTester class contains a main method that calls the changeValues method in a ParameterModifier object. Two of the parameters to changeValues are Num objects, each of which simply stores an integer value. The other parameter is a primitive integer value.

## LISTING 7.15

```
//****************************************************************
//  ParameterTester.java      Author: Lewis/Loftus
//
//  Demonstrates the effects of passing various types of parameters.
//****************************************************************

public class ParameterTester
{
    //-------------------------------------------------------------
    //  Sets up three variables (one primitive and two objects) to
    //  serve as actual parameters to the changeValues method. Prints
    //  their values before and after calling the method.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        ParameterModifier modifier = new ParameterModifier();

        int a1 = 111;
        Num a2 = new Num (222);
        Num a3 = new Num (333);

        System.out.println ("Before calling changeValues:");
        System.out.println ("a1\ta2\ta3");
        System.out.println (a1 + "\t" + a2 + "\t" + a3 + "\n");

        modifier.changeValues (a1, a2, a3);

        System.out.println ("After calling changeValues:");
        System.out.println ("a1\ta2\ta3");
        System.out.println (a1 + "\t" + a2 + "\t" + a3 + "\n");
    }
}
```

## OUTPUT

Before calling changeValues
 a1      a2      a3
 111     222     333

Before changing the values:
 f1      f2      f3
 111     222     333

## LISTING 7.15 continued

```
After changing the values:
f1      f2      f3
999    888    777

After calling changeValues:
a1      a2      a3
111    888    333
```

Listing 7.16 shows the ParameterModifier class, and Listing 7.17 shows the Num class. Inside the changeValues method, a modification is made to each of the three formal parameters: the integer parameter is set to a different value, the value stored in the first Num parameter is changed using its setValue method, and a new

## LISTING 7.16

```
//****************************************************************
// ParameterModifier.java    Author: Lewis/Loftus
//
// Demonstrates the effects of changing parameter values.
//****************************************************************

public class ParameterModifier
{
    //-------------------------------------------------------------
    // Modifies the parameters, printing their values before and
    // after making the changes.
    //-------------------------------------------------------------
    public void changeValues (int f1, Num f2, Num f3)
    {
        System.out.println ("Before changing the values:");
        System.out.println ("f1\tf2\tf3");
        System.out.println (f1 + "\t" + f2 + "\t" + f3 + "\n");

        f1 = 999;
        f2.setValue(888);
        f3 = new Num (777);

        System.out.println ("After changing the values:");
        System.out.println ("f1\tf2\tf3");
        System.out.println (f1 + "\t" + f2 + "\t" + f3 + "\n");
    }
}
```

```java
/*******************************************************
// Num.java      Author: Lewis/Loftus
//
// Represents a single integer as an object.
/*******************************************************

public class Num
{
    private int value;

    //---------------------------------------------------
    // Sets up the new Num object, storing an initial value.
    //---------------------------------------------------
    public Num (int update)
    {
        value = update;
    }

    //---------------------------------------------------
    // Sets the stored value to the newly specified value.
    //---------------------------------------------------
    public void setValue (int update)
    {
        value = update;
    }

    //---------------------------------------------------
    // Returns the stored integer value as a string.
    //---------------------------------------------------
    public String toString ()
    {
        return value + "";
    }
}
```

Num object is created and assigned to the second Num parameter. These changes are reflected in the output printed at the end of the changeValues method.

However, note the final values that are printed after returning from the method. The primitive integer was not changed from its original value, because the change was made to a copy inside the method. Likewise, the last parameter still refers to its original object with its original value. This is because the new Num object created in the method was referred to only by the formal parameter. When

the method returned, that formal parameter was destroyed and the Num object it referred to was marked for garbage collection. The only change that is “permanent” is the change made to the state of the second parameter. Figure 7.5 shows the step-by-step processing of this program.

## STEP 1

Before invoking changeValues

## STEP 2

```
tester.changeValues (a1, a2, a3);
```

## STEP 3

```
f1 = 999;
```

## STEP 4

```
f2.setValue (888);
```

## STEP 5

```
f3 = new Num (777);
```

## STEP 6

After returning from changeValues

□ = Undefined

## FIGURE 7.5 Tracing the parameters in the ParameterTesting program

## SELF-REVIEW QUESTIONS *(see answers in Appendix N)*

**SR 7.18** What is method decomposition?

**SR 7.19** Answer the following questions about the `PigLatinTranslator` class.
- a. No constructor is defined. Why not?
- b. Some of the defined methods are private. Why?
- c. A `Scanner` object is declared in the `translate` method. What is it used to scan?

**SR 7.20** Identify the resultant sequence of calls/returns of `PigLatinTranslator` support methods when `translate` is invoked with the following actual parameters.
- a. `"animal"`
- b. `"hello"`
- c. `"We are the champions"`

**SR 7.21** How are objects passed as parameters?

## 7.8 Method Overloading

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
