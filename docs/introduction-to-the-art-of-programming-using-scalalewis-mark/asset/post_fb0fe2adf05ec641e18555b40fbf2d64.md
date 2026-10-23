
and more importantly, if the method is abstract and you do not implement it, that will generate a syntax error unless the class is labeled as abstract.

To help you understand this second reason, let us look at an example of why Scala requires the override keyword in the first place when you are overriding a method. Consider this version of Rectangle.

```
class Rectangle(val width: Double, val height: Double, c: Color) extends Shape(c) {
  def area: Double = width * height
  def circumference: Double = 2.0 * (width + height)
  override def draw(g: Graphics) { // ERROR: Not really an override
    g.setPaint(color)
    g.fill(new Rectangle2D.Double(0.0, 0.0, width, height))
  }
}
```

The override keyword has been dropped from area and circumference because they are abstract in the supertype. There is a comment on the draw method telling you that it will not compile. Can you tell what is wrong? There is a very subtle error here that most people would miss without the comment and it is quite possible that you are having a hard time identifying it even with the comment. The error is that `g` is listed as being type Graphics instead of Graphics2D. That kind of little typo is very easy to do when you are coding and, if it were not a syntax error, it could produce a logic error that is very difficult to track down. Scala requires override in this usage so that it will be a syntax error if you change the type. In the situation where override is not required because the method in the supertype is abstract, a typo in the argument or method name will leave that method unimplemented, which will generate a different error indicating that the class has to be abstract because some method is abstract.

## 19.2.6 traits

The class and object constructs are not the only ways to create new types in Scala. A third option, which is significant to us in this chapter, is the trait. A trait is very similar to an abstract class in many ways. The two primary differences are that traits can not take arguments and you can inherit from more than one trait.

It was not specifically said above, but you might have noticed there was no description of how to list multiple classes after extends. This was not an oversight, you are not allowed to list multiple classes there. You are allowed to follow the class with multiple traits or just have one or more traits. The various types you inherit from are separated by the with keyword.

To understand why you would want to do this, consider the following example. Imagine you are writing software to simulate people moving through a building to help with designing the space. You have a type called Person that represents everyone that can be in the simulation. The company you are working for knows there are certain categories of people who behave in significantly different ways that the simulation must handle. For example, they need types for Parent, Child, and GeneralAdult. The need for facilities in the building means they also need types for Male and Female. This last part creates a problem for single inheritance because you want to be able to represent a type Father by inheriting from Parent and Male. The subtype relationship makes sense there, but if both of those types are written as classes, you will not be able to use them both.

There are two ways that you could approach this problem with traits. A somewhat standard inheritance scheme might use the following structure.

```
trait Person { ... }
trait Parent extends Person { ... }
trait Male extends Person { ... }
class Father extends Parent with Male { ... }
```

Here both Parent and Male are subtypes of Person and Father inherits from both. In this case Person has to be a trait. This is because a trait can only inherit from other traits, not classes. Below that, either Parent or Male could have been a class, but not both because Father could not inherit from both of them then. Without a pressing reason to make one a class, the choice of a trait provides consistency.

An alternate approach to constructing these types could be to use the traits as mix-in types. Here is what the code could look like.

```
class Person { ... }
trait Parent { ... }
trait Male { ... }
class Father extends Person with Parent with Male { ... }
```

In this construction, both the Parent and Male types are traits that do not inherit from the Person. Instead, they are mixed in with the Person to create the Father. This approach is perhaps a bit more advanced and, if the Parent and Male types involve code that requires them to know they will be used with a Person, you will need to use self-types, which are discussed in appendix B. What matters now is that you be aware that this option exists so that, as we build different inheritance hierarchies, you will understand what is going on.

### trait or abstract class?

A standard question programmers deal with in writing Scala is whether to choose an abstract class or a trait when coding an abstract type that will be used with inheritance. The general rule of thumb here is to prefer a trait because it allows the flexibility of multiple inheritance. While it cannot take arguments, any values that you would want to provide as arguments can be put into the trait and left undefined, so that the class that implements them in the end will have to provide values for those.

## 19.2.7 final

When something is abstract, it basically means that it has to be “overridden” in a subclass.¹ There are times when it is also useful to be able to say that something cannot be overridden, or changed in a subtype. This requirement can be enforced with the final keyword. You can use final to modify member data or methods that you do not want to be changed in subtypes. It can also be used to modify a whole class when you do not want to allow there to be any subtypes of that class.

You might wonder why you would want to make something final. One answer to this question is that you want to preserve some type of behavior in the current implementation that should not be altered in subtypes. It can also be a way of telling things that use a class that there is no possibility of getting different behavior from an object of that type than what they would get from that specific type.

The most common example of a place where you should use **final** to preserve a behavior in a type is when a class defines a type that is immutable. The strengths of immutable types, and how they can be used to simplify code, is something that has been addressed quite a bit already in this book. Without inheritance, if you wrote a type to be immutable, you knew that any object of that type could be passed to other code without fear of it being changed.² With inheritance, that does not automatically hold true unless you make the **class** final. The reason for this is that subtypes could add mutable data and/or override methods such that the new implementations include some reference to a mutable state.

To help you understand this, consider the following example class.

```
class CharInStrComp(str: String) {
    def positionCompare(str2: String, index: Int): Int = {
        if (index >= str.length) {
            if (index >= str2.length) 0 else 1
        } else if (index >= str2.length) -1 else {
            str(index).compareTo(str2(index))
        }
    }
}
```

This class is immutable. Technically it does not even have member data to mutate. So if you have an object created from this class, it can be passed around freely. With inheritance, though, it would be possible to do this.

```
class CntCharInStrComp(str: String) extends CharInStrComp(str) {
    var cnt = 0
    override def positionCompare(str2: String, index: Int): Int = {
        cnt += 1
        super.positionCompare(str2, index)
    }
}
```

If you make an instance of CntCharInStrComp, it can be used in any place that wants a CharInStrComp. The only problem is that if this is done in a place where the code relies on objects being immutable, that code can now break because it is being passed an object that is mutable. To prevent this from happening, the original version should be made **final**, as is shown here.

```
final class CharInStrComp(str: String) {
    def positionCompare(str2: String, index: Int): Int = {
        if (index >= str.length) {
            if (index >= str2.length) 0 else 1
        } else if (index >= str2.length) -1 else {
            str(index).compareTo(str2(index))
        }
    }
}
```

Now any attempt to make a subtype, whether mutable or not, will produce an error.

The **final** keyword is often underused in programming. However, it is good to get into the habit of making things **final** when there are not supposed to be subtypes or when something should not be overridden. This is not only a safe practice to get into; code that is labeled as **final** can sometimes be compiled to faster implementations as well.

2. We will also see in chapter 21 that such objects can be used safely across multiple threads.
