# Calling an object's methods

Calling a string's equals method is like getting a purchase's total. With both equals and total, you use your old friend, the dot. For example, in Listing 17-3, you write

```
System.out.println(onePurchase.total);
```

and in Listing 18-5, you write

```
if (password.equals(userInput))
```

A dot works the same way for an object's variables and its methods. In either case, a dot takes the object and picks out one of the object's parts. It works whether that part is a piece of data (as in onePurchase.total) or a method (as in password.equals).

# Combining and using data

At this point in the chapter, I can finally say, "I told you so." Here's a quotation from Chapter 17:

> > A class is a design plan; it describes the way in which you intend to combine and use pieces of data.

A class can define the way you use data. How do you use a password and a user's input? You check to see whether they're the same. That's why Java's String class defines an equals method.

![](bbox=[0.15, 0.78, 0.25, 0.9])

An object can be more than just a bunch of data. With object-oriented programming, each object possesses copies of methods for using that object.

# Static Methods

You have a fistful of checks. Each check has a number, an amount, and a payee. You print checks like these with your very own laser printer. To print the checks, you use a Java class. Each object made from the Check class has three variables (number, amount, and payee). And each object has one method (a print method). You can see all this in Figure 18-7.