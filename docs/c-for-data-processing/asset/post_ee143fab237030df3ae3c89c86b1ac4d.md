
```csharp
class AccountTest
{
    public static void Main ()
    {
        Account test = new Account();
        test.PayInterest (50);
        Console.WriteLine ("Balance:" + test.GetBalance());
    }
}
```

The AccountTest class has a static member method called Main. We know that this is the method which is called to run the program. It is part of the class AccountTest. If I made fifty AccountTest instances, they would all share the same Main method. In terms of C# the keyword static flags a member as being part of the class, not part of an instance of the class. I will write that down again in a posh font,

> > “A static member is a member of the class, not a member of an instance of the class”

I don't have to make an instance of the AccountTest class to be able to use the Main method. This is how my program actually gets to work, in that when it starts it has not made any instances of anything, and so this method must be there already, otherwise it cannot run.

Static does not mean 'cannot be changed'. I think this is time for more posh font stuff:

> > Static does not mean "cannot be changed".

Members of a class which have been made static can be used just like any other member of a class. Either a data member or a method can be made static.

## 4.6.2 Using a static data member of a class

Perhaps an example of static data would help at this point. Consider the interest rates of our bank accounts. The customer has told us that one of the members of the account class will need to be the interest rate on accounts. In the program we can implement this by adding another member to the class which holds the current interest rate:

```csharp
public class Account
{
    public decimal Balance ;
    public decimal InterestRateCharged ;
}
```

Now I can create accounts and set balances and interest rates on them. (of course if I was doing this properly I'd make this stuff private and provide methods etc, but I'm keeping things simple just now).

```csharp
Account RobsAccount = new Account();
RobsAccount.Balance = 100;
RobsAccount.InterestRateCharged = 10;
```

The snag is I've been told that the interest rate is held for all the accounts. If the interest rate changes it must change for all accounts. This means that to implement the change I'd have to go through all the accounts and update the rate. This would be tedious, and if I missed one account, possibly expensive.

I solve the problem by making the interest rate member static:

```csharp
public class Account
{
    public decimal Balance ;
    public static decimal InterestRateCharged ;
}
```

The interest rate is now part of the class, not part of any instance. This means that I have to change the way that I get hold of it:

```csharp
Account RobsAccount = new Account();
RobsAccount.Balance = 100;
Account.InterestRateCharged = 10;
```

Since it is a member of the class I now have to use the class name to get hold of it instead of the name of the instance reference.

### Programmer's Point: Static Data Members are Useful and Dangerous

When you are collecting metadata about your project you should look for things which can be made static. Things like the limits of values (the largest age that you are going to permit a person to have) can be made static. There might be a time where the age limit changes, and you don't want to have to update all the objects in your program.

But of course, as Spiderman's uncle said, "With great power comes great responsibility." You should be careful about how you provide access to static data items. A change to a single static value will affect your entire system. So they should always be made private and updated by means of method calls.

## 4.6.3 Using a static method in a class

We can make methods static too. We have been doing this for ages with the Main method. But you can also use them when designing your system. For example, we might have a method which decides whether or not someone is allowed to have a bank account. It would take in their age and income. It would then return true or false depending on whether these are acceptable or not:

```csharp
public bool AccountAllowed ( decimal income, int age )
{
    if ( ( income >= 10000 ) && ( age >= 18 ) )
    {
        return true;
    }
    else {
        return false;
    }
}
```

This checks the age and income; you must be over 17 and have at least 10000 pounds income to be allowed an account. The snag is that, at the moment, we can't call the method until we have an Account instance. We can solve this by making the method static:

```csharp
public static bool AccountAllowed ( decimal income, int age )
{
    if ( ( income >= 10000 ) && ( age >= 18 ) )
    {
        return true;
    }
    else {
        return false;
    }
}
```

Now the method is part of the class, not an instance of the class. I can now call the method by using the class name:

```csharp
if ( Account.AccountAllowed ( 25000, 21 ) )
{
    Console.WriteLine ( "Allowed Account" );
}
```

This is nice because I have not had to make an instance of the account to find out if one is allowed.

### Using member data in static methods

The Allowed method is OK, but of course I have fixed the age and income methods into it. I might decide to make the method more flexible:

```csharp
public class Account
{
    private decimal minIncome = 10000;
    private int minAge = 18;

    public static bool AccountAllowed(decimal income, int age)
    {
        if ( ( income >= minIncome ) && ( age >= minAge ) )
        {
            return true;
        }
        else
        {
            return false;
        }
    }
}
```

This is a better design, in that I now have members of the class which set out the upper limits of the age and income. However it is a bad program, since the class above will not compile:

```
AccountManagement.cs(19,21): error CS0120: An object reference is required for the nonstatic field, method, or property 'Account.minIncome'
AccountManagement.cs(19,43): error CS0120: An object reference is required for the nonstatic field, method, or property 'Account.minAge'
```

As usual, the compiler is telling us exactly what is wrong; using language which makes our heads spin. What the compiler really means is that "a static method is using a member of the class which is not static."

If that doesn't help, how about this. The members minIncome and minAge are held within instances of the Account class. However, a static method can run without an instance (since it is part of the class). The compiler is unhappy because in this situation the method would not have any members to play with. We can fix this (and get our program completely correct) by making the income and age limits static as well:

```csharp
public class Account
{
    private static decimal minIncome ;
    private static int minAge ;

    public static bool AccountAllowed(decimal income, int age)
    {
        if ( ( income >= minIncome ) && ( age >= minAge ) )
        {
            return true;
        }
        else
        {
            return false;
        }
    }
}
```

If you think about it, this makes perfect sense. The limit values should not be held as members of a class, since we want them to be the same for all instances of the class, therefore, making them static is what we should have done in the first place.

### Programmer's Point: Static Method Members can be used to make Libraries

Sometimes in a development you need to provide a library of methods to do stuff. In the C# system itself there are a huge number of methods to perform maths functions, for example sin and cos. It makes sense to make these methods static, in that in this situation all we want is the method itself, not an instance of a class. Again, when you are building your system you should think about how you are going to make such methods available for your own use.

## BANK NOTES: STATIC BANK INFORMATION

The kind of problems that we can use static to solve in our bank are:

**static member variable:** The manager would like us to be able to set the interest rate for all the customer accounts at once. A single static member of the Account class will provide a variable which can be used inside all instances of the class. But because there is only a single copy of this value this can be changed and thereby adjust the interest rate for all the accounts. Any value which is held once for all classes (limits on values are another example of this) is best managed as a static value. The time it becomes impossible to use static is when the manager says "Oh, accounts for five year olds have a different interest rate from normal ones." At this point we know we can't use static because we need to hold different values for some of the instances.

**static member method:** the manager tells us that we need a method to determine whether or not a given person is allowed to have an account. I can't make this part of any Account instance because at the time it runs an account has not been generated. I must make it static, so that it can execute without an instance.

## 4.7 The Construction of Objects

We have seen that our objects are created when we use new to bring one into being:

```csharp
test = new Account();
```

If you look closely at what is happening you might decide that what is happening looks quite a bit like a method call.

This is actually exactly what is happening. When an instance of a class is created the C# system makes a call to a constructor method in that class. The constructor method is a member of the class and it is there to let the programmer get control and set up the contents of the shiny new object. One of the rules of the C# game is that every single class must have a constructor method to be called when a new instance is created.
