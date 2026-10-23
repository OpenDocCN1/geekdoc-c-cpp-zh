class we likely want both to be constant so we should change the class declaration to the following.

```
class Student(val name:String, val id:String) {
```

If you make this change you can use the print statement shown above without an error.

# 16.1.1.2 Visibility

The possibility of things being visible or not is pretty much new to us, but it is a very important aspect of object-oriented programming because it allows you to hide details of the way an object works away from the code that uses the class. The value of this is that you can change those details without causing problems for the code that depends on the class to work. In the case of member data, you can also hide away details that you do not want other parts of code to have free access to.

A great demonstration of this last part comes in the form of a bank account. Let us consider the simplest possible class that we might write to represent a bank account.

```
class Account {
    var balance=0
}
```

This class does not take any arguments when it is constructed and, as a result, the parentheses have been left off. It has one piece of member data, an Int for the balance. As you might recall from chapter 3, money should be stored in Ints because the arithmetic of the Double type is inaccurate due to the limited precision. This representation is simple, but it has a significant drawback. The member balance is a var that can be set by any code that gets hold of an Account object. For a real bank program that would not be acceptable. The balance can not just be any value. For example, negative numbers generally are not allowed. In addition, changes to the balance are typically supposed to happen in specific operation, deposits and withdrawals. Those operations can enforce certain rules and, for a real bank, would log any changes to the balance so that it is possible to go back and figure out what happened. While we could make functions for those operations, there would be nothing that forces programmers to use them. It would be possible for a programmer to “get lazy” at some point and access the balance directly. The results of this in banking software could be quite extreme.

The ability to force access to data to occur through certain methods is one of the most significant capabilities of object-orientation as a way of improving software construction and controlling complexity. The real benefit of this capability is to take responsibility for proper usage away from the users of the objects. If the only ways to use the object are through methods or data that is safe for them to use, then they know they can not mess it up and do not have to worry about that. Instead, they can focus on the logic that they are working on.

So how do we accomplish this in our classes? We do it by setting the visibility of members. There are three main levels of visibility in Scala and they are very similar to what you will find in other class-based object-oriented languages.

+   • Public - This means that something can be accessed by any code inside of outside of the class. In Scala this is the default visibility for elements so there is no keyword for it.

+   • private - This means that the member can only be accessed inside the class. Attempts to get to the member outside the class will result in a syntax error. If