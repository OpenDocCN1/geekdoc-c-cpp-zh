# Chapter 84: Lambda expressions

# Section 84.1: Lambda Expressions as Shorthand for Delegate Initialization

```
public delegate int ModifyInt(int input);
ModifyInt multiplyByTwo = x => x * 2;
```

The above Lambda expression syntax is equivalent to the following verbose code:

```
public delegate int ModifyInt(int input);

ModifyInt multiplyByTwo = delegate(int x){
    return x * 2;
};
```

# Section 84.2: Lambda Expression as an Event Handler

Lambda expressions can be used to handle events, which is useful when:

+   - The handler is short.
+   - The handler never needs to be unsubscribed.

A good situation in which a lambda event handler might be used is given below:

```
smtpClient.SendCompleted += (sender, args) => Console.WriteLine("Email sent");
```

If unsubscribing a registered event handler at some future point in the code is necessary, the event handler expression should be saved to a variable, and the registration/unregistration done through that variable:

```
EventHandler handler = (sender, args) => Console.WriteLine("Email sent");

smtpClient.SendCompleted += handler;
smtpClient.SendCompleted -= handler;
```

The reason that this is done rather than simply retyping the lambda expression verbatim to unsubscribe it (-=) is that the C# compiler won't necessarily consider the two expressions equal:

```
EventHandler handlerA = (sender, args) => Console.WriteLine("Email sent");
EventHandler handlerB = (sender, args) => Console.WriteLine("Email sent");
Console.WriteLine(handlerA.Equals(handlerB)); // May return "False"
```

Note that if additional statements are added to the lambda expression, then the required surrounding curly braces may be accidentally omitted, without causing compile-time error. For example:

```
smtpClient.SendCompleted += (sender, args) => Console.WriteLine("Email sent");
emailSendButton.Enabled = true;
```

This will compile, but will result in adding the lambda expression (sender, args) => Console.WriteLine("Email sent"); as an event handler, and executing the statement emailSendButton.Enabled = true; immediately. To fix this, the contents of the lambda must be surrounded in curly braces. This can be avoided by using curly braces from the start, being cautious when adding additional statements to a lambda-event-handler, or surrounding the lambda in round brackets from the start: