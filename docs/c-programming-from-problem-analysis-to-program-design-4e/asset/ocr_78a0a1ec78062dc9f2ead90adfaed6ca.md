As you review Example 4–18, notice that properties were defined in the CarpetCalculator class called `NoOfSqYard`, `PricePerSqYard` and `Price`. The `Price` and `PricePerSqYard` properties are both tied to the `pricePerSqYard` data member, which was defined with an access mode of `private`. Rarely will you want to associate two separate properties to a single data member. `Price` was defined to illustrate that you do not have to follow the standard naming convention. Recall that data members are named using Camel case, while property identifiers follow the Pascal case convention; thus, the only difference normally in their names is the first character. `pricePerSqYard` can be referenced in the class where it is defined, but because it is defined with an access mode of `private`, it cannot be referenced outside of the defining class.

In the second class, `CarpetCalculatorApp`, an object of the `CarpetCalculator` class is instantiated. The object identifier is `berber`. The object is instantiated with the `new` operator as shown here:

```
CarpetCalculator berber = new CarpetCalculator(17.95);
```

Since a double value, 17.95, is sent in as an argument to the constructor, the one argument constructor is used. 17.95 goes into `price` and that value is placed in the `private` data member `pricePerSqYard` as shown here in the constructor:

```
public CarpetCalculator(double price)
{
    pricePerSqYard = price;
}
```

In order to change berber’s `pricePerSqYard` in the `CarpetCalculatorApp` class, you must use the property `PricePerSqYard`. The `private` `pricePerSqYard` data member is not accessible in the second class. The `PricePerSqYard` was changed to 25.99 with the statement shown below:

```
berber.PricePerSqYard = 25.99;
```

The `PricePerSqYard` property has `get` and `set` clauses. In order for classes that instantiate objects of the `CarpetCalculator` class to change the objects’ `pricePerSqYard`, they use the `set` clause associated with the public property. The object’s `private` data members’ value (i.e., `pricePerSqYard`) is retrieved through the `public` property’s `get` clause.

Next, in the `Main()` method of the `CarpetCalculatorApp` class, the mutator method `SetNoOfSqYards()` was invoked. Notice that this method, like the property reference above had to be invoked with an object. It also offers a `public` access mode; thus, it is available in classes instantiating objects of the `CarpetCalculator` class. The object was `berber` for this example. A `public` property could have been defined for `noOfSqYards` instead of a mutator method. The `public` property `NoOfSqYards` would have been tied to the `private` `noOfSqYards` data member.