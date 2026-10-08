# Chapter 4 Introduction to Classes, Objects, Methods and strings

![](bbox=[0.199, 0.125, 0.8, 0.303])

# 4.6 Account Class with a Property Rather Than Set and Get Methods

Our first Account class contained a private instance variable name and public methods SetName and GetName that enabled a client to assign to and retrieve from an Account's name. C# provides a more elegant solution—called properties—to accomplish the tasks. A property encapsulates a set accessor for storing a value in a variable and a get accessor for getting the value of a variable.³ In this section, we will revisit the AccountTest class to demonstrate how to interact with an Account object containing a public Name property, then will present the updated Account class and take a detailed look at properties.

# 4.6.1 Class AccountTest Using Account's Name Property

Fig. 4.5 shows the updated AccountTest class that uses Account's Name property (declared in Fig. 4.6) to get and set an Account's name instance variable. This app produces the same output as the one in Fig. 4.1, assuming the user once enters Jane when prompted to enter a name.

```
// AccountTest.cs
// Creating and manipulating an Account object with properties.
using System;
class AccountTest
{
    static void Main()
    {
        // create an Account object and assign it to myAccount
        myAccount = new Account();
    }
```

Fig. 4.5 | Creating and manipulating an Account object with properties. (Part 1 of 2)

+   * In subsequent chapters, you'll see that properties are not required to have both a set and a get.