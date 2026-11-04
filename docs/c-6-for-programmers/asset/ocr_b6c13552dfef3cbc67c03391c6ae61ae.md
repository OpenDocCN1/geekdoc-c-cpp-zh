methods and properties. They manipulate the instance variables belonging to particular objects of the class.

Instance variables are declared *inside* a class declaration but *outside* the bodies of the class’s methods and properties. Line 7

```
```java
private string name; // instance variable
```
```

declares instance variable name of type string *outside* the bodies of methods SetName and GetName. If there are many Account objects, each has its own name. Because name is an instance variable, it can be manipulated by each of the class’s methods and properties. Clients of class Account—that is, any other code that calls the class’s methods (such as class AccountTest’s Main method in Fig. 4.1)—cannot access the name instance variable because it’s declared private. However, clients can access Account’s public methods SetName and GetName. These methods can access private instance variable name. We discuss private and public in Section 4.3.6, then discuss why this architecture of private instance variables and public *access methods* is powerful in more detail in Section 4.5.

> **Good Programming Practice 4.1**
> 
> We prefer to list a class’s instance variables first in the class’s body, so that you see the names and types of the variables before they’re used in the class’s methods and properties. You can list the class’s instance variables anywhere in the class outside its method (and property) declarations, but scattering the instance variables can lead to hard-to-read code.

![](bbox=[0.16, 0.39, 0.215, 0.431])

# *null—the Default Initial Value for string Variables*

Every instance variable has a *default initial value*—a value provided by C# if you do not specify the instance variable’s initial value. Thus, instance variables are not required to be explicitly initialized before they’re used in a program—unless they must be initialized to values other than their default values. The default value for an instance variable of type string (like name in this example) is **null**, which we discuss further in Chapter 7 when we consider so-called *reference types*. When you use `Console.Write` or `Console.WriteLine` to display a string variable that contains the value null, no text is displayed on the screen—this is why line 13 in Main (Fig. 4.1) did not display a name the first time we called myAccount’s GetName method.

# ### 4.3.4 SetName Method

Let’s walk through the code of method SetName’s declaration (Fig. 4.2, lines 10–13):

```
```java
public void SetName(string accountName)
{
    name = accountName; // store the account name
}
```
```

The first line of each method declaration (line 10) is the *method header*. The method’s *return type* (which appears to the left of the method’s name) specifies the type of data the method returns to its *caller* after performing its task. The return type `void` (line 10) indicates that method SetName completes its task, it does not return (i.e., give back) any information to its *calling method*—in this example, line 18 of the Main method (Fig. 4.1). As you’ll soon see, Account method GetName does return a value.