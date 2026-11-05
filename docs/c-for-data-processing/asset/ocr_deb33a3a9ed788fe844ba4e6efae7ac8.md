```
if ( Account.AccountAllowed ( 25000, 21 ) )
{
    Console.WriteLine ( "Allowed Account" );
}
```

This is nice because I have not had to make an instance of the account to find out if one is allowed.

# Using member data in static methods

The Allowed method is OK, but of course I have fixed the age and income methods into it. I might decide to make the method more flexible:

```
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