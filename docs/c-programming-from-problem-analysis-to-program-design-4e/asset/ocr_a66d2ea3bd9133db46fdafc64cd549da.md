A standard naming convention is to add “Set” to the front of the instance variable identifier; that name becomes the mutator method name. In Example 4-5, the instance variable being changed is noOfSqYards; the identifier for the mutator is SetNoOfSqYards( ).

# Other Instance Methods

You wrote class methods in Chapter 3. Class methods manipulate data by having information passed in as arguments through parameters. That is not necessary with instance methods. Instance method members of a class can directly access private data members of the same class. It is through instance methods that private data is manipulated. Examine the instance method CalculateAverage( ) shown in Example 4-7. Notice there are no parameters for the method. CalculateAverage( ) can use score1, score2, and score3 because they belong to the same class.

# EXAMPLE 4.7

```
public double CalculateAverage()
{
    return (score1 + score2 + score3) / 3.0;
}
```

As illustrated in Example 4-7, CalculateAverage( ) can directly access score1, score2, and score3. It was not necessary to send that data into the method via a parameter.

Also notice exam average is not one of the data members. The average is not stored. This was done to avoid potential inconsistencies with the data. Normally, any time information can be calculated from other values, it is best to define a method to perform the behavior. By defining a method as opposed to storing the average, it will reduce the chance of inaccurate or inconsistent data. If one of the object’s scores is changed, it would be easy to fail to change the average if it were a data member. This is where the potential for inconsistent data pops up. If average is only available through invoking a method, the current values of score1, score2, and score3 will always be used.

# Property

One of the underlying themes of object-oriented programming is encapsulation, which states that the internal representation of an object is generally hidden, thus member data are defined with private access. Typically, the only way to access, inspect, or manipulate the object’s data is through the object’s public methods. As you just read, many languages provide mutators, or setters that enable the data to be changed. They provide accessors or getters that enable the data to be retrieved. Another option is to define and use properties. C# introduced properties. A property looks like a data field, but it does not directly represent a storage location. Properties are more closely aligned to methods. They provide a way to change or retrieve private member data. Example 4-8 includes the property for noOfSqYards and pricePerSqYard data members.