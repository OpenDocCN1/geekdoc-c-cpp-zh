throughout this guide so all you need for now is just to have a basic understanding of them. This is the part of the code we are talking about now:

```
class Program
{
static void Main(string[] args)
{
And then to close it
}
}
```

Fundamentally, a class is something like a blueprint for a specific object type. Most of the code that you write will belong to one of these classes and, in our case, that class is called “Program”. As we go through this guide, you will be making a lot of classes because they are one of the most critical parts of C# and other OOP or Object-Oriented Programming languages.

Inside a class, we have methods – you will see these called functions in other languages. More about these later. For now, a method is a block of code that does a specific job. What our compiler is going to be looking for is the “Main” method.

The rest of what you see on that line:

```
static void Main(string[] args)
```

This is known as the “method signature. This is where specific properties are defined for the method and these are also vital to the C# compiler when it comes to finding the “Main” method – do NOT modify these in any way.

We’ll talk about these later in the guide. What you need to know right now is that the compiler will look for this line so it knows where your program starts.