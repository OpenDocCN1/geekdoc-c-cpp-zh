# Object Oriented Programming using C#

To allow this method EnrolStudent() could be overloaded and an alternative method provided as...

```
EnrolStudent(String name, String coursecode)
```

At run time the method invoked will depend upon the parameter list provided. Thus a call to

```
EnrolStudent("Fred", "123 Abbey Gardens", "G700")
```

the first method would be used.

# Activity 1

Imagine a method WithdrawCash() could be used as part of a banking system. This method could take two parameters
: the account identity (String) and the amount of cash required by the user (int). Thus the full method signature would be
:

```
WithdrawCash(String accountID, int amount).
```

Identify another variation of the WithdrawCash() method that takes a different parameter list that may be a useful variation
of the method above.

# Feedback 1

An alternative method also used to withdraw cash could be WithdrawCash(String accountID) where no specified amount is
provided by default £100 is withdrawn.

These methods essentially perform the same operation but by overloading this method we have made the system more
flexible - users now have a choice they can specify the amount of cash to be withdrawn or they can accept the default sum
sspecified.

Overloading methods don't just provide more flexibility for the user they also provide more flexibility for programmers
who may have the job of extending the system in the future and thus overloading methods can make the system more
future proof and robust to changing requirements.

Constructors can be overloaded as well as ordinary methods.