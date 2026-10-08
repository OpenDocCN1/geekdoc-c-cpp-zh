# CHAPTER 13: BECOMING FAMILAR WITH THE CONCEPT OF INHERITANCE

As mentioned in the previous chapter, one of the most important aspects of any oriented programming language is classes. In the same way, inheritance is a key concept in object oriented programming.

As C# is such a language, you will have to utilize inheritance sooner than later. In, the entirety of the .NET framework has been built upon the concept of inheritance. It is responsible for the expression that everything is an object.

Inheritance, in simple terms, enables you to create classes that can inherit attributes from their parent classes. In C#, even a simple number can be an instance of a class that inherits from the parent class, System.Object.

Inheritance can be a bit advanced for some beginners. However, it is better to become familiar with it sooner than later because of the roles it plays in C# programming. Here is an example that illustrates the use of inheritance.

```
public class Animal\{
    public void Greet()
    {
        Console.WriteLine("Hello! I'm some kind of animal.");
    }
}
public class Cat: Animal
{
n}
```

As you can see, an Animal class has been defined first along with a simple method