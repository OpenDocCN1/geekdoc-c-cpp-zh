declared (such as string Salary = "Not enough" in Listing 6.5). Therefore, assignment within a constructor will override any value assigned at declaration time. This subtlety can lead to a misinterpretation of the code by a casual reader who assumes the value after instantiation is the one assigned in the field declaration. Therefore, it is worth considering a coding style that does not mix both declaration assignment and constructor assignment within the same class.

# ## ADVANCED TOPIC

# ### Implementation Details of the new Operator

Internally, the interaction between the new operator and the constructor is as follows. The new operator retrieves "empty" memory from the memory manager and then calls the specified constructor, passing a reference to the empty memory to the constructor as the implicit this parameter. Next, the remainder of the constructor chain executes, passing around the reference between constructors. None of the constructors have a return type; behaviorally they all return void. When execution of the constructor chain is complete, the new operator returns the memory reference, now referring to the memory in its initialized form.

# ### Default Constructors

When you add a constructor explicitly, you can no longer instantiate an Employee from within Main() without specifying the first and last names. The code shown in Listing 6.28, therefore, will not compile.

# **LISTING 6.28:** Default Constructor No Longer Available

```
```
class Program
{
    static void Main()
    {
        Employee employee;
        // ERROR: No overload because method 'Employee'
        // takes '0' arguments
        employee = new Employee();

        // ...
    }
}
```
```