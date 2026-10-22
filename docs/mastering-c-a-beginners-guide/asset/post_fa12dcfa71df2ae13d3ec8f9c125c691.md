
It is essential to know that the implementation of the logic in classes is encapsulated (hidden) inside them. For the programmer, it is vital what they do, not how they do it, and for this reason, a significant part of the classes is not publicly accessible (public). With system classes, the implementation is sometimes not accessible at all to the programmer. Thus, new layers of abstraction are built, which is one of the fundamental principles in OOP.

## Creating and Using Objects

Let us focus on creating and using objects in our programs, and it is done with already well defined classes and mostly with system classes from .NET Framework.

The creation of objects from preliminarily defined classes during program implementation is done by the operator new. The newly created object is often assigned to the variable from type coinciding with the class of the object. We will note that in this assignment, the object is not copied, and only a reference to the newly created object is recorded in the variable (its address in the memory). Here is a simple example of how it works:

```
Cat someCat = new Cat();
```

The variable someCat of type Cat, we appropriate the newly created instance of the class Cat. The variable someCat remains in the stack, and its value (the instance of the class Cat) remains in the managed heap.

Now, we will take up a slightly different variant of the example above in which we set parameters when creating the object:

```
Cat someCat = new Cat("Jack", "brown");
```

In this case, we would like the objects someCat to represent a cat whose name is “Jack” and is brown. We indicate this by using the words “Jack” and “brown,” written in the brackets after the name of the class.

When creating an object with the operator new, two things would happen: Memory is set aside for this object, and its data members are initialized. The initialization is performed by a unique method called constructor. In the example above, the initializing parameters are really parameters of the constructor of the class.

As the member variables name and color of the class Cat are of a reference type (of the class String), they are also recorded in the dynamic memory (heap), and in the object itself are kept their references (addresses/ pointers).

## Releasing the Objects

An essential feature of working with objects in C# is that there is no need to manually tear them down and release the memory taken up by them. This is possible because of the embedded in .NET CLR system for cleaning the memory (garbage collector), which takes care of releasing unused objects instead of us. Objects to which there is no reference in the program at a particular moment instinctively released, and the memory they take up is released. This way, many potential bugs, and problems are controlled. If we would like to release a specific object manually, we have to destroy the reference to it, for example, this way:

```
someCat = null;
```

## Access to Fields of an Object

The operator . (dot) placed between the names of the object and the name of the field (or the property) does the access to the fields and properties of a given object.¹ The operator is not necessary in case we access field or property of a given class in the body of a method of the same class.

We can either access the fields and the properties to extract data from them or assign new data. In a property, the access is implemented in the same way as in a field—C# gives us this ability. The keywords achieve this get and set in the definition of the property, which performs respectively extraction of the value of the property and assignment of a new value. In the description of the class Cat (given above), the properties are Name and Color.

### Access to the Memory and Properties of an Object—Example

We will give an example of using a property of an object and using the already explained above class Cat. We develop an instance myCat of the class Cat and assign "James" to the property Name. After that, we print on the standard output a formatted string with the name of our Cat. You can see an implementation of the example:

```
class CatManipulating
{
    static void Main()
    {
        Cat myCat = new Cat();
```

> ¹ Svetlin Nakov and Team,(2013),Fundamentals of Computer Programming with C#, *creating and using objects*

```
myCat.Name = "James";
Console.WriteLine("The name of my cat is {0}.",
    myCat.Name);
}
}
```

## Calling Methods of Objects

Calling the methods of a given object is done through the invocation operator () and with the help of the operator . (dot). The operator dot is not obligatory only if the method is called in the body of another method of the same class. Calling a method is performed by its name followed by () or (<parameters>) for the case when we give it some arguments.

Now is the moment to mention that methods of classes have access modifiers private, public, or protected with which the potential to call them could be restricted. For now, it is enough to know that the access modifier public does not introduce any restrictions for calling the method, i.e., makes it publicly available.

## Calling Methods of Objects—Example

We will complement the example we already provided as we call the method SayMiau of the class Cat. Here is the result:

```
class CatManipulating
{
    static void Main()
    {
        Cat myCat = new Cat();
```

as with methods. The compiler automatically chooses the appropriate constructor according to the given bunch of parameters when creating the object. We use the principle of the best match.

## Calling Constructors—Example

Let’s remind again at the definition of the class Cat and, more specifically, at the two constructors of the class:

```
public class Cat
{
    // Field name
    private string name;
    // Field color
    private string color;
    ...
    // Parameterless constructor
    public Cat()
    {
        this.name = "Unnamed";
        this.color = "gray";
    }
    // Constructor with parameters
    public Cat (string name, string color)
    {
        this.name = name;
        this.color = color;
    }
}
```

We are going to use these constructors to show the usage of constructors with and without parameters. For the class Cat defined that way, we will create its instances by each of the two constructors. One of the objects will be an ordinary

undefined cat, and the other is our brown Cat Jack. After that, we will execute the method SayMiau for each of the cats and analyze the result. Source code follows:

```
class CatManipulating
{
    static void Main()
    {

Cat someCat = new Cat();
        someCat.SayMiau();
        Console.WriteLine("The color of
cat {0} is {1}.",
            someCat.Name, someCat.Color);

        Cat someCat = new Cat("Jack",
"brown");
        someCat.SayMiau();
        Console.WriteLine("The color of
cat {0} is {1}.",
            someCat.Name, someCat.Color);
    }
}
```

As a result of the program’s execution the following text is printed on the standard output:

- Cat Unnamed said: Miauuuuuu!
- The color of Cat Unnamed is gray.
- Cat Jack said: Miauuuuuu!
- The color of Cat Johnny is brown.
- Static Fields and Methods.

The data members, which we considered until now, implement states of the objects and are directly related to specific classes. In OOP, special categories fields and methods are associated with the data type (class), not the specific instance (object). We call them static members because they are independent of concrete objects. Furthermore, they are used without the need to develop an instance of the class in which they are defined. They can be fields, methods, and constructors. Let’s consider shortly static members in C#.

A static field or method in a given class is defined with the keyword static, placed before the type of the field or the type of returned value of the method. When defining a static constructor, the word static is placed before the name of the constructor.

## When to Use Static Fields and Methods

To find the answers to this question, we must understand the difference between static and non-static members. We are going to consider into detail what it is.

We have already explained the main difference between the two types of members. Let’s paraphrase the class as a category of objects and the object as a representative of this category. Then the static members reflect the state and the behavior of the category itself, and the non-static members represent the state and the behavior of the separate representatives of that particular category.

Now, we will heed special attention to the initialization of static and non-static fields. We are already aware that non-static fields are initialized with the call to the class’s constructor when creating an instance of it—either inside the constructor’s body or outside. However, the
