indicating that something urgent has happened, and a way of specifying the code that should be run when the urgent event happens. Events, in conjunction with delegates, provide the infrastructure with which you can implement systems that follow this approach.

You’ll start by looking at delegates.

# Understanding delegates

A delegate is a reference to a method. It is a very simple concept with extraordinarily powerful implications. Let me explain.

Note
Delegates are so named because they “delegate” processing to the referenced method when they are invoked.

Typically, when you write a statement that invokes a method, you specify the name of the method (and possibly specify the object or structure to which the method belongs). It is clear from your code exactly which method you are running and when you are running it. Look at the following simple example that calls the performCalculation method of a Processor object (what this method does or how the Processor class is defined is immaterial for this discussion):

Click here to view code image

```
Processor p = new Processor();
p.performCalculation();
```

A delegate is an object that refers to a method. You can assign a reference to a method to a delegate in much the same way that you can assign an int value to an int variable. The next example creates a delegate named performCalculationDelegate that references the performCalculation method of the Processor object. I have deliberately omitted some elements of the statement that declares the delegate because it is more important to understand the concept rather than worry about the syntax (you will see the full syntax shortly).

Click here to view code image

```
Processor p = new Processor();
delegate ... performCalculationDelegate ...;
performCalculationDelegate = p.performCalculation;
```

Keep in mind that the statement that assigns the method reference to the delegate does not run the method at that point; there are no parentheses after the method name, and you do not specify any parameters (if the method takes them). This is just an assignment statement.

Having stored a reference to the performCalculation method of the Processor