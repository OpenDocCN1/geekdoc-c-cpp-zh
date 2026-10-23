to act. Indeed, the prefix unary operations for +, -, !, and ~ are part of the Scala libraries. You can write methods in a class that are interpreted as prefix unary operators. To do so, simply name the method unary_op, where op is replaced by +, -, !, or ~. So if you wanted your own negation you could create a method called unary_-.

# 16.1.4.3 Property Assignment Methods

Back in the bank account example we said that having a method that starts with the word get followed by the value you were getting was the Java style of doing things and that in Scala you simply name a method with the name you want people to see for the property. In our example this was balance. In Java style the partner to the get method is a set method. In Scala that counterpart to set is an assignment method. The advantage of the assignment method is that it allows you to set a property using normal assignment syntax. To create an assignment operator, write a method with the name prop_-, where prop is the name of the property.

To help you understand this, let us assume that you did want to be able to enter something like myAccount.balance = 700. We had this ability with the public var, but we decided that was too little control. We could get that back by adding the following method.

```
```
def balance_=(b:Int) = bal=b
```
```

Thanks to the way Scala handles assignment operators, this will let both of the following lines work.

```
```
myAccount.balance = 700
myAccount.balance += 40
```
```

So doing += will work like a deposit and -= will work like a withdraw. The downside is that neither returns a Boolean to let you know if it worked. As written, neither checks the value being deposited or withdrawn either.

This particular method leaves things too open. We might as well have the var because we are doing exactly what the var would do. However, the advantage of an assignment method is that it can be more complex and have more logic behind it. For example, the balance-= method could be altered to the following.

```
```
def balance_=(b:Int) = {
if(b>=0) {
if(b>bal) withdraw(bal-b) else deposit(b-bal)
} else false
}
```
```

This version will reuse the code from withdraw or deposit include any error checking, logging, etc. It also throws in checking so that assignments to invalid balances will not go through.

Note that you only include a set method for properties that are mutable so there are many situations where they are left off. If you are programming in a more functional style, you will not have these assignment methods. It is only when objects specifically need to be able to mutate that these are helpful. The real advantage in that case is that the code can look like a normal assignment, but will call the method that can do various types of error checking.