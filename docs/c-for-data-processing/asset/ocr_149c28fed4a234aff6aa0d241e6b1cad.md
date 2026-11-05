Note that types I create (like SeaState) will be highlighted by the editor in a blue colour which is not quite the same as keywords.

This shows that these items are extra types I have created which can be used to create variables, but they are not actually part of the C# language, like keywords are. It is important that you understand what is happening here. Previously we have used types that are part of C#, for example int and double. Now we have reached the point where we are actually creating our own data types which can be used to hold data values that are required by our application.

# 4.2.2 Creating an enum type

The new enum type can be created outside any class and creates a new type for use in any of my programs:

```
using System;
enum TrafficLight
{
    Red,
    RedAmber,
    Green,
    Amber
};
class EnumDemonstration
{
    public static void Main ()
    {
        TrafficLight light ;
        light = TrafficLight.Red;
    }
}
```

Every time that you have to hold something which can take a limited number of possible values, or states (for example OnSale, UnderOffer, Sold, OffTheMarket etc) then you should think in terms of using enumerated types to hold the values.

# Programmer's Point: Use enumerated types

Enumerated types are another occasion where everyone benefits if you use them. The program becomes simpler to write, easier to understand and safer. You should therefore use them a lot.

For the bank you want to hold the state of an item as well as other information about the customer. For example, we could have the states "Frozen", "New", "Active", "Closed" and "Under Audit" as states for our bank account. If this is the case it is sensible to create an enumerated type which can hold these values and no others

```
enum AccountState
{
    New,
    Active,
    UnderAudit,
    Frozen,
    Closed
};
```

We now have a variable which can hold state information about an account in our bank. Every account will contain a variable of type AccountState which represents the state of that account.