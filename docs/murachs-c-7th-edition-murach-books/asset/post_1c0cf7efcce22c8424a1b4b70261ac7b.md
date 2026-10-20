
## How to create a delegate
### Using an anonymous method
```
ProductList.ChangeHandler myDelegate =
delegate (ProductList products)
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
myDelegate(products);
```
### Using a lambda expression
```
ProductList.ChangeHandler myDelegate = products =>
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
myDelegate(products);
```

## How to wire an event
### Using an anonymous method
```
products.Changed += delegate (ProductList products)
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
```
### Using a lambda expression
```
products.Changed += products =>
{
    Debug.WriteLine("The products list has changed!");
    for (int i = 0; i < products.Count; i++) { ... }
};
```

## Description
- An *anonymous method* is a method without a name. You can use an anonymous method when you create a delegate instead of specifying a named method. If the method is only called from one place, this can help simplify your code.
- A *lambda expression* is similar to an anonymous method, but it uses the lambda operator instead of the delegate keyword.
- You can also wire an anonymous method or lambda expression to an event. When you do that, you should place the code in the class constructor, or if the class is a form, the Load event handler.

## How to overload operators
The ProductList class in figure 13-2 uses overloaded operators. Specifically, this class overloads the + and - operators so you can add products to and remove products from the product list using these operators rather than the Add() and Remove() methods. The following topics explain how you implement overloaded operators like these.

### An introduction to operator overloading
Figure 13-9 presents some basic information about *operator overloading*. First, you should know that you can overload both unary and binary operators. The most common operators you can overload are listed in this figure.

C# defines the meanings of these operators for built-in types such as decimal, int, string, and DateTime. However, for user-defined types such as the Product class presented in the last chapter or the ProductList class presented in this chapter, these operators are either undefined or are defined in ways that may not be appropriate for the class. For example, the + operator isn’t defined for user-defined types, but the == operator is. By default, if you compare two object variables using the == operator, they’re considered equal if they refer to the same object.

With operator overloading, you can create your own implementations of C# operators that are appropriate for your classes. For example, a more appropriate definition of the == operator for the Product class would be to consider two Product variables equal if they refer to objects with the same Code, Description, and Price properties.

As the syntax at the top of this figure shows, you use the operator keyword to declare an operator. In the operator declaration, you specify the return type, which indicates the type of object that’s returned by the operation. In most cases, the return type is the same as the class that contains the declaration (for example, Product in the Product class). Then, you specify the operator you want to define, followed by one or two operands depending on whether the operator is a unary or a binary operator.

Notice that operators are always declared as static. That way, they can deal with null operands properly. That will make more sense when you see the code for the overloaded == operator.

Overloaded operators often depend on methods that are defined by the class. In figure 13-10, for example, you’ll see that the + operator for the ProductList class uses the Add() method of the class to add a product to the list. Then, in figure 13-11, you’ll see that the == and != operators for the Product class are implemented by overriding the Equals() method of the Object class, which is inherited by all other classes.

### The syntax for overloading unary operators
```
public static returnType operator unary-operator(type operand)
```

### The syntax for overloading binary operators
```
public static returnType operator
    binary-operator(type-1 operand-1, type-2 operand-2)
```

### Common operators you can overload
#### Unary operators
```
+ - ! ++ -- true false
```

#### Binary operators
```
+ - * / % & | == != > < >= <=
```

### The Equals() method of the Object class
| Method | Description |
|---|---|
| Equals(object) | Returns a Boolean value that indicates whether the current object refers to the same instance as the specified object. If that’s not what you want, you can override this method as shown in figure 13-11. |
| Equals(object1, object2) | A static version of the Equals() method that compares two objects to determine if they refer to the same instance. |

### The GetHashCode() method of the Object class
| Method | Description |
|---|---|
| GetHashCode() | Returns an integer value that’s used to identify objects in a hash table. If you override the Equals() method, you must also override the GetHashCode() method. |

## Description
- You use the *operator* keyword to *overload an operator* within a class. For example, you might overload the + operator in the ProductList class so it can be used to add products to the list. You might also overload the == and != operators in the Product class so you can compare two Product objects to see if they contain identical data rather than whether they refer to the same instance.
- You can overload all of the unary and binary operators shown above, as well as some that aren’t presented in this book. When you overload a binary operator, *operand-1* is the operand that appears to the left of the operator, and *operand-2* is the operand that appears to the right of the operator.
- *Overloaded operators* are always static so they can deal with null operands properly.
- When you overload relational operators like == and !=, you need to provide your own versions of the Equals() and GetHashCode() methods. See figure 13-11 for details.

### Part of a ProductList class that overloads the + operator
```
public class ProductList
{
    private List<Product> products;

    public void Add(Product p)
    {
        products.Add(p);
    }

    public static ProductList operator + (ProductList pl, Product p)
    {
        pl.Add(p);
        return pl;
    }
    .
    .
}
```

### Code that uses the + operator of the ProductList class
```
ProductList products = new ProductList();
Product p = new Product("C#", "Murach's C#", 59.50m);
products = products + p;
```

### Another way to use the + operator
```
products += p;
```

### Code that uses an expression-bodied operator
```
public ProductList Add(Product p)
{
    products.Add(p);
    return this;
}

public static ProductList operator + (ProductList pl, Product p) =>
    pl.Add(p);
```

## Description
- You can overload the built-in arithmetic operators so they perform customized functions on objects created from the class that defines them.
- You should overload only those arithmetic operators that make sense for a class. For example, it’s reasonable to overload the + operator for the ProductList class as a way to add products to a product list. But it doesn’t make sense to overload the * or / operators for this class.
- You don’t overload the += or -= operators separately. Instead, these operators are handled automatically by the overloaded + and - operators.
- An operator that simply returns an expression or executes a single statement can be coded as an *expression-bodied operator*. Expression-bodied operators became available with C# 6.0.

## How to overload relational operators
Figure 13-11 shows that relational operators are often more difficult to overload than arithmetic operators. Here, the first example shows how to implement the == operator for the Product class so you can compare products based on their values rather than on object references. The two objects that will be compared are passed as arguments to this operator.

The operator starts by using the Equals() method of the Object class to check both objects to see if they’re equal to null. This implementation of the Equals() method is based on reference, not value. As a result, it lets you test an object to see if it is null. This testing is necessary to prevent the overloaded == operator from throwing an exception if one of the operands is null.

If both operands are null, the == operator returns true. If the first operand is null but the second one isn’t, it returns false. And if the first operand isn’t null, the == operator calls the Equals() method of the first operand to compare it with the second operand, and then returns the result of the comparison.

Notice that the declaration for the Equals() method includes the override keyword. That means that it overrides the Equals() method defined by the Object class that every class inherits. In the next chapter, you’ll learn how to work with inheritance. Then, you’ll be able to understand how this code works.

The Equals() method starts by testing the object that’s passed to it, in this case, the second operand of the == operator, for a null. If this object is null, the Equals() method returns false. That makes sense, because no object should be considered equal to a null.

If the object that’s passed to the Equals() method isn’t null, this method casts the object to a Product object named p. Then, it compares its own Code, Description, and Price values with the Code, Description, and Price values of the p object. If all three properties are equal, it returns true. Otherwise, it returns false.

When you overload a comparison operator, you must also overload the operator that performs the opposite operation. If, for example, you overload the == operator, you must also overload the != operator. Similarly, if you overload the < operator, you must also overload the > operator. The code that’s used to implement the != operator in the Product class is also shown in this figure. As you can see, this operator defines itself in terms of the == operator. That way, you can be sure that these operators return consistent results.

The last method that’s required when you overload the == operator is the GetHashCode() method. Like the Equals() method, this method overrides the GetHashCode() method that’s defined by the Object class. The main requirement for the GetHashCode() method is that it must always return the same value for any two objects that are considered equal by the Equals() method. The easiest way to accomplish that is to combine the values that are used for comparison in the Equals() method to create a string, and then return the hash code of that string.

The second example in this figure shows how you can use the == operator to compare two Product objects. First, two object variables named p1 and p2 are created from the Product class with identical values. Then, the products are
