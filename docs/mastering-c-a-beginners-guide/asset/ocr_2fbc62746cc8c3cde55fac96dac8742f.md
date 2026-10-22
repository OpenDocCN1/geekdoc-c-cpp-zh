# Access to Fields of an Object

The operator does the access to the fields and properties of a given object.¹ (dot) placed between the names of the object and the name of the field (or the property). The operator is not necessary in case we access field or property of a given class in the body of a method of the same class.

We can either access the fields and the properties to extract data from them or assign new data. In a property, the access is implemented in the same way as in a field—C# gives us this ability. The keywords achieve this get and set in the definition of the property, which performs respectively extraction of the value of the property and assignment of a new value. In the description of the class Cat (given above), the properties are Name and Color.

# *Access to the Memory and Properties\nof an Object—Example*

We will give an example of using a property of an object and using the already explained above class Cat. We develop an instance myCat of the class Cat and assign "James" to the property Name. After that, we print on the standard output a formatted string with the name of our Cat. You can see an implementation of the example:

```
class CatManipulating
{
    static void Main()
    {
        Cat myCat = new Cat();
```

> ¹ Svetlin Nakov and Team,(2013),Fundamentals of Computer Programming with C#, *creating and using objects*