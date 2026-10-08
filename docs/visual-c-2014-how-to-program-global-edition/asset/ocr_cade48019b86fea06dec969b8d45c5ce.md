# 4.3 Account Class with an Instance Variable and Set and Get Methods

# ### SetName’s Parameter

Our car analogy from Section 1.6 mentioned that pressing a car’s gas pedal sends a message to the car to perform a task—make the car go faster. But how fast should the car accelerate? The further down you press the pedal, the faster the car accelerates. So the message to the car includes both the task and information that helps the car perform that task. This information is known as a parameter—the value helps the car determine how fast to accelerate. Similarly, a method can require one or more parameters that represent the data it needs to perform its task.

MethodName declares the parameter accountName—which receives the name passed to it as an argument. When line 18 in Fig. 4.1

```
myAccount.setName(theName); // put theName in myAccount object
```

executes, the argument value in the parentheses (i.e., the value stored in theName) is copied into the corresponding parameter (accountName) in the method’s header (line 10 of Fig. 4.2). In Fig. 4.1 sample execution, we entered "Jane Green" for theName, so "Jane Green" was copied into the accountName parameter.

# ### SetName Parameter List

Parameters like accountName are declared in a parameter list located in the parentheses following the method name. Each parameter must specify a type (e.g., string) followed by a name. When there are multiple parameters, they are placed in a comma-separated list, as

```
(type name1, type2 name2, ...)
```

The number and order of arguments in a method declaration must match the number and order of parameters in the method parameter list.

# ### SetName Method Body

Every body is defined by an opening left brace (Fig. 4.2, line 11) and a closing right brace (line 12). Within these braces are one or more statements that perform the task. In this case, the method body contains a single statement (line 12)

```
name = accountName; // store the account name
```

assigns the accountName parameter’s value (a string) to the class’s instance variable, storing the name in the object for which SetName was called—myAccount in this example’s Main program. After line 12 executes, program execution reaches the method’s body (line 13), the method returns to its caller.

# ### Parameters Are Local Variables

In Chapter 3, we declared all of an app’s variables in the Main method. Variables declared in a particular method (such as Main) are local variables which can be used only in that method. Each method can access its own local variables, not those of other methods. When a method terminates, the values of its local variables are lost. A method’s parameters are also local variables of the method.

+   2. We used different names for the SetName method’s parameter (accountName) and the instance variable (name). It’s common in industry to use the same name for both. We’ll show you how to do this without ambiguity in Section 10.4.