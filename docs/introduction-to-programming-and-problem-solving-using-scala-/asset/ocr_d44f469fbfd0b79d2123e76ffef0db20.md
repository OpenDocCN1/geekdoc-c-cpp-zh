# 10.1 User Defined Types

What we need to break away from the limitations of using tuples to deal with groupings of data is the ability to define our own types that have meaningful names. Tuples definitely have their place, and they are very useful in those situations, such as when you need to return 2 or 3 values from a function. However, there are many times when it would be handy to create a type specifically for a particular purpose. Then we could give you a name that indicated its purpose and have the compiler check for us that we were using that type in the proper way.

User defined types are common feature of programming languages and have been there for decades. Scala provides two constructs for creating user defined types: classes and traits. For this chapter, in order to keep things simple, we will only consider a specific type of one of them, the case class.

In chapter 7 we define a type as a collection of values and the operations that can be performed on them. User defined types typically take the form of other types. This makes them fundamentally similar to just using a tuple. Where they prove to be more than just a tuple is the control they give you in determining what can be done with them. We will remain somewhat limited in this regard for now, but even with those limitations you find that our defined types provide a significant boost to our programming capabilities.

# 10.2 case classes

The simplest way to start with user defined types in Scala is with case classes. We will start with two examples that were mentioned above: a 3-D point and a student with some grades.

```
case class Point3D(x:Double, y:Double, z:Double)
case class Student(name:String, assignments:List[Double], tests:List[Double], quizzes:List[Double])
```

The first one declares a type called Point3D that stores inside of three Doubles that are named x, y and z. The second declares a type called Student that has a name which is String and different Lists of Double to use as grades.
There can be more to the declaration of a case class, but for now we will limit our syntax to that which begins with the keywords “case class”. After that is the name you want to give the type. This could be any valid Scala name, but it is customary to begin types with uppercase letters and use camel naming so all subsequent words begin with uppercase letters. After that it is a list of name/type pairs in parentheses. The format of these is just like the arguments to a function. The elements of this list give the name and types of the values stored in this new type. The values stored in a class are called MEMBERS and a case class is a class.

> Using a type declaration, it is possible to give a more meaningful name to a tuple, but it is still an equivalent type, so the compiler will accept any tuple of the correct structure and does not help you much finding errors.