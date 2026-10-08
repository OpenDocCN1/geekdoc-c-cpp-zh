```
Transaction t2 = new Transaction("002", "9/10/2012", 451900.00);

t1.showTransaction();

t2.showTransaction();

Console.ReadKey();
}
}
```

On executing the code shown above, the following result is produced.

Transaction: 001
Date: 8/10/2012
Amount: 78900
Transaction: 002
Date: 9/10/2012
Amount: 451900

# Starting With Polymorphism

Literally, polymorphism can be defined as having multiple forms. However, in the object oriented programming methodology, polymorphism is generally described as having one interface but multiple functions. Now, polymorphism can be either static or dynamic.

# Static Polymorphism

Static binding is the mechanism by which a function is linked with an object while the program is being compiled. In other words, the decision is taken during compile time. In C#, there are two techniques by which static polymorphism can be implemented.