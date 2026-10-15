```
EmailCustomer("123@sample.com");

EmailCustomer("456@sample.com");

EmailCustomer("789@sample.com");

EmailCustomer("101@sample.com");

EmailCustomer("155@sample.com");

// What if we have thousands?
```

Even with all of the code we see here, we'd still only email a handful of customers and reach thousands of people. This simply would not work. We need a better way to process large sets of data and rapidly perform the same tasks over and over. C# allows us to use iteration statements to accomplish this. Iteration statements, or loops, as they're generally called, enable us to execute a block of code over and over until a certain condition is met. Or in other words, they iterate over a set of data or statements to achieve a result. There are several types of loops, but the most standard example is called a for loop. The for statement executes a block of code repeatedly as long as some condition evaluates to true. Later in