![](bbox=[0.18, 0.08, 0.82, 0.4])

Here the chain is built as following:

+   - Logic class holds first receiver which is Logger
+   - Logger class holds the next receiver which is Emailer
+   - Emailer class have null receiver denoting end of chain

Following code depicts the above chain creation:

```
Logic logic = new Logic();
logic.Receiver = new Logger(new Emailer(null));
```

Note: Please note that the advantage of this pattern is decoupling of sender and receiver. The sender does not think about the right receiver. Instead it will pass the request and the appropriate receiver should process it. The above example can be written using a list of receivers in the Logic class with a Boolean property mentioning whether the message is processed or not.

# Comparing Observer and Chain of Responsibility

In the case of Observer pattern all the registered receivers will get the request. Each of the receivers is interested in processing it. But in chain of responsibility the request is passed until it is not processed.