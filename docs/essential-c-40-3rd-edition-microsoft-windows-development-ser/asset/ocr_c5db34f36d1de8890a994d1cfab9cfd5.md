```
employee.Salary);
// ...
}
```

Notice that the new operator returns the type of the object being instantiated (even though no return type or return statement was specified explicitly in the constructor’s declaration or implementation). In addition, you have removed the initialization code for the first and last names because that occurs within the constructor. In this example, you don’t initialize Salary within the constructor, so the code assigning the salary still appears.

Developers should take care when using both assignment at declaration time and assignment within constructors. Assignments within the constructor will occur after any assignments are made when a field is declared (such as string Salary = "Not enough" in Listing 5.5). Therefore, assignment within a constructor will override any value assigned at declaration time. This subtlety can lead to a misinterpretation of the code by a casual reader whereby he assumes the value after instantiation is assigned at declaration time. Therefore, it is worth considering a coding style that does not mix both declaration assignment and constructor assignment within the same class.

# ADVANCED TOPIC

# Implementation Details of the new Operator

Internally, the interaction between the new operator and the constructor is as follows. The new operator retrieves memory from the memory manager and then calls the specified constructor, passing the initialized memory to the constructor. Next, the remainder of the constructor chain executes, passing around the initialized memory between constructors. None of the constructors have a return type (behaviorally they all return void). When execution completes on the constructor chain, the new operator returns the memory reference, now referring to the memory in its initialized form.