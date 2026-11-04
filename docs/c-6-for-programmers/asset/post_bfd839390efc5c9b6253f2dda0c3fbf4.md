
## *SetName's Parameter*

Our car analogy from Section 1.2 mentioned that pressing a car's gas pedal sends a message to the car to perform a task—make the car go faster. But how fast should the car accelerate? The farther down you press the pedal, the faster the car accelerates. So the message to the car includes both the task to perform and information that helps the car perform that task. This information is known as a parameter—the parameter's value helps the car determine how fast to accelerate. Similarly, a method can require one or more parameters that represent the data it needs to perform its task.

Method SetName declares the String parameter accountName—which receives the name that's passed to SetName as an argument. When line 18 in Fig. 4.1

```
myAccount.SetName(theName); // put theName in the myAccount object
```

executes, the argument value in the call's parentheses (i.e., the value stored in theName) is copied into the corresponding parameter (accountName) in the method's header (line 10 of Fig. 4.2). In Fig. 4.1's sample execution, we entered "Jane Green" for theName, so "Jane Green" was copied into the accountName parameter.

## *SetName Parameter List*

Parameters like accountName are declared in a parameter list located in the required parentheses following the method's name. Each parameter must specify a type (e.g., String) followed by a parameter name (e.g., accountName). When there are multiple parameters, they are placed in a comma-separated list, as in

```
(type1 name1, type2 name2, ...)
```

The number and order of arguments in a method call must match the number and order of parameters in the method declaration's parameter list.

## *SetName Method Body*

Every method body is delimited by an opening left brace (Fig. 4.2, line 11) and a closing right brace (line 13). Within the braces are one or more statements that perform the method's task(s). In this case, the method body contains a single statement (line 12)

```
name = accountName; // store the account name
```

that assigns the accountName parameter's value (a string) to the class's name instance variable, thus storing the account name in the object for which SetName was called—myAccount in this example's Main program.2 After line 12 executes, program execution reaches the method's closing brace (line 13), so the method returns to its caller.

## *Parameters Are Local Variables*

In Chapter 3, we declared all of an app's variables in the Main method. Variables declared in a particular method's body (such as Main) are local variables which can be used only in that method. Each method can access only its own local variables, not those of other methods. When a method terminates, the values of its local variables are lost. A method's parameters are also local variables of the method.

2. We used different names for the SetName method's parameter (accountName) and the instance variable (name). It's common idiom in industry to use the same name for both. We'll show you how to do this without ambiguity in Section 10.4.

### 4.3.5 GetName Method

Method GetName (lines 16–19)

```csharp
public string GetName()
{
    return name; // returns name's value to this method's caller
}
```

*returns* a particular Account object's name to the caller—a string, as specified by the method's return type. The method has an empty parameter list, so it does not require additional information to perform its task. When a method with a return type other than `void` is called and completes its task, it *must* return a result to its caller. A statement that calls method GetName on an Account object expects to receive the Account's name.

The return statement in line 18

```csharp
return name; // returns name's value to this method's caller
```

passes the string value of instance variable `name` back to the caller, which can then use the returned value. For example, the statement in line 21 of Fig. 4.1

```csharp
Console.WriteLine($"myAccount's name is: {myAccount.GetName()}");
```

uses the value returned by GetName to output the name stored in the myAccount object.

### 4.3.6 Access Modifiers private and public

The keyword **private** (line 7 of Fig. 4.2)

```csharp
private string name; // instance variable
```

is an access modifier. Instance variable `name` is private to indicate that name is accessible *only* to class Account's methods (and other members, like properties, as you'll see in subsequent examples). This is known as *information hiding*—the instance variable name is hidden and can be used *only* in class Account's methods (SetName and GetName). Most instance variables are declared private.

This class also contains the **public** access modifier (line 10)

```csharp
public void SetName(string accountName)
```

and line 16

```csharp
public string GetName()
```

Methods (and other class members) that are declared **public** are "available to the public." They can be used

- by methods (and other members) of the class in which they're declared,
- by the class's clients—that is, methods (and other members) of any other classes (in this app, class AccountTest's `Main` method is the client of class Account).

In Chapter 11, we'll introduce the protected access modifier.

### Default Access for Class Members

By default, everything in a class is private, unless you specify otherwise by providing access modifiers.

> **Error-Prevention Tip 4.1**
>
> *Making a class's instance variables private and its methods (and as you'll see, properties) public and accessing those instance variables only through the class's methods and properties facilitates debugging, because problems with data manipulations are localized to the methods (and properties).*

> **Common Programming Error 4.1**
>
> *An attempt by a method that's not a member of a particular class to access a private member of that class is a compilation error.*

### 4.3.7 Account UML Class Diagram

We'll often use UML class diagrams to summarize a class's attributes and operations. In industry, UML diagrams help systems designers specify systems in a concise, graphical, programming-language-independent manner, before programmers implement the systems in specific programming languages. Figure 4.3 presents a UML class diagram for class Account of Fig. 4.2.

![](img/3f5ef6be1748bb746e5f71a483bba4d0_111_0.png)

Fig. 4.3 | UML class diagram for class Account of Fig. 4.2.

*Top Compartment*

In the UML, each class is modeled in a class diagram as a rectangle with three compartments. In this diagram the top compartment contains the class name Account centered horizontally in boldface type.

*Middle Compartment*

The middle compartment contains the class's attribute names, which correspond to the instance variables of the same names in C#. The single instance variable name in Fig. 4.2 is private in C#, so the UML class diagram lists a minus sign (-) UML access modifier before the attribute's name. Following the attribute's name are a colon and the attribute type, in this case string.

*Bottom Compartment*

The bottom compartment contains the class's operations, SetName and GetName, which correspond to the methods of the same names in C#. The UML models operations by listing the operation name preceded by a UML access modifier, for example, + SetName. This plus sign (+) indicates that SetName is a public operation in the UML (because it's a public method in C#). Operation GetName is also a public operation.

## Return Types

The UML indicates an operation's return type by placing a colon and the return type *after* the parentheses following the operation name. Method SetName does not return a value (because it returns void in C#), so the UML class diagram does not specify a return type after the parentheses of this operation. Method GetName has a string return type. The UML has its own data types similar to those of C#—for simplicity, we use the C# types.

## Parameters

The UML models a parameter by listing the parameter name, followed by a colon and the parameter type in the parentheses after the operation name. Account method SetName has a string parameter called accountName, so the class diagram lists

```
accountName : string
```

between the parentheses following the method name. Operation GetName does not have any parameters, so the parentheses following the operation name in the class diagram are empty, just as they are in the method's declaration in line 16 of Fig. 4.2.

## 4.4 Creating, Compiling and Running a Visual C# Project with Two Classes

When you create the project for this app, you should rename Program.cs to AccountTest.cs and add the Account.cs file to the project. To set up a project with two classes:

- 1. Create a Console Application as you did in Chapter 3. We named this chapter's projects Account1, Account2, Account3 and Account4, respectively.
- 2. Rename the project's Program.cs file to AccountTest.cs. Replace the autogenerated code with class AccountTest's code (Fig. 4.1).
- 3. Right click the project name in the Solution Explorer and select Add > Class... from the pop-up menu.
- 4. In the Add New Item dialog's Name field, enter the new file's name (Account.cs), then click Add. In the new Account.cs file, replace the auto-generated code with class Account's code from Fig. 4.2.

You can open each class in the Visual Studio editor by double clicking the filename in the Solution Explorer window.

You must compile the classes in Figs. 4.1 and 4.2 before you can execute the app. This is the first time you've created an app with *multiple classes*. Class AccountTest has a Main method; class Account does not. The IDE automatically recognizes as the app's entry point the class that contains Main. When you select Build > Build Solution in Visual Studio, the IDE compiles all the files in the project to create the executable app. If both classes compile correctly—that is, no compilation errors are displayed—you can then run the app by typing *Ctrl + F5* to execute the AccountTest class's Main method. If you do not build the app before running it, typing *Ctrl + F5* will build the app first and run the app only if there are no compilation errors.
