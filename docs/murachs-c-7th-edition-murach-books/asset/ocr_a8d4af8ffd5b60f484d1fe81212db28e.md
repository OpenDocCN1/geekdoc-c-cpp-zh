# How to overload relational operators

Figure 13-11 shows that relational operators are often more difficult to overload than arithmetic operators. Here, the first example shows how to implement the == operator for the Product class so you can compare products based on their values rather than on object references. The two objects that will be compared are passed as arguments to this operator.

The operator starts by using the Equals() method of the Object class to check both objects to see if they’re equal to null. This implementation of the Equals() method is based on reference, not value. As a result, it lets you test an object to see if it is null. This testing is necessary to prevent the overloaded == operator from throwing an exception if one of the operands is null.

If both operands are null, the == operator returns true. If the first operand is null but the second one isn’t, it returns false. And if the first operand isn’t null, the == operator calls the Equals() method of the first operand to compare it with the second operand, and then returns the result of the comparison.

Notice that the declaration for the Equals() method includes the override keyword. That means that it overrides the Equals() method defined by the Object class that every class inherits. In the next chapter, you’ll learn how to work with inheritance. Then, you’ll be able to understand how this code works.

The Equals() method starts by testing the object that’s passed to it, in this case, the second operand of the == operator, for a null. If this object is null, the Equals() method returns false. That makes sense, because no object should be considered equal to a null.

If the object that’s passed to the Equals() method isn’t null, this method casts the object to a Product object named p. Then, it compares its own Code, Description, and Price values with the Code, Description, and Price values of the p object. If all three properties are equal, it returns true. Otherwise, it returns false.

When you overload a comparison operator, you must also overload the operator that performs the opposite operation. If, for example, you overload the == operator, you must also overload the != operator. Similarly, if you overload the < operator, you must also overload the > operator. The code that’s used to implement the != operator in the Product class is also shown in this figure. As you can see, this operator defines itself in terms of the == operator. That way, you can be sure that these operators return consistent results.

The last method that’s required when you overload the == operator is the GetHashCode() method. Like the Equals() method, this method overrides the GetHashCode() method that’s defined by the Object class. The main requirement for the GetHashCode() method is that it must always return the same value for any two objects that are considered equal by the Equals() method. The easiest way to accomplish that is to combine the values that are used for comparison in the Equals() method to create a string, and then return the hash code of that string.

The second example in this figure shows how you can use the == operator to compare two Product objects. First, two object variables named p1 and p2 are created from the Product class with identical values. Then, the products are