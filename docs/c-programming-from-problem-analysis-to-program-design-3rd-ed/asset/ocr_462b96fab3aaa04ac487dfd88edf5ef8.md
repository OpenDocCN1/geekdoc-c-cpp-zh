# Table 4-1 Value type defaults

| Value type | Default value |
|---|---|
| bool | false |
| byte | 0 |
| char | '\0' (null) |
| decimal | 0.0M |
| double | 0.0D |
| float | 0.0F |
| int | 0 |
| long | 0L |
| short | 0 |
| uint | 0 |
| ulong | 0 |
| ushort | 0 |

![](bbox=[0.17, 0.55, 0.22, 0.62])

Attempting to add a value to an uninitialized variable in C# is not allowed.

The second call to the constructor sends two arguments. An object named pile is created, and an object named berber is created with the third constructor. The actual argument of 17.95 is used to initialize the private member pricePerSqYard.

# Calling Accessor and Mutator Methods

Accessor and mutators are instance methods. All instance methods are called in exactly the same manner as class methods, with one exception. If the method is being called from another class that has instantiated an object of the class, the method name is preceded by the object name. If another member of the same class is using the method, all that is needed is the name of the method. You never precede an instance method with the name of the class like you do with static class methods. In order to call the method in another class, a specific object must be associated with it.

One of the methods of the CarpetCalculator class is SetNoOfSqYards( ). Another class, called CarpetCalculatorApp, has instantiated an object of the CarpetCalculator class by using the one argument constructor shown previously in Example 4-4. The call to the constructor to instantiate the berber object is shown again as follows:

```
CarpetCalculator berber = new CarpetCalculator(17.95);
```