
## 10.1 User Defined Types

What we need to break away from the limitations of using tuples to deal with groupings of data is the ability to define our own types that have meaningful names. Tuples definitely have their place, and they are very useful in those situations, such as when you need to return 2 or 3 values from a function. However, there are many times when it would be handy to create a type specifically for a particular purpose. Then we could give you a name that indicated its purpose and have the compiler check for us that we were using that type in the proper way.

User defined types are common feature of programming languages and have been there for decades. Scala provides two constructs for creating user defined types: classes and traits. For this chapter, in order to keep things simple, we will only consider a specific type of one of them, the case class.

In chapter 7 we define a type as a collection of values and the operations that can be performed on them. User defined types typically take the form of other types. This makes them fundamentally similar to just using a tuple. Where they prove to be more than just a tuple is the control they give you in determining what can be done with them. We will remain somewhat limited in this regard for now, but even with those limitations you find that our defined types provide a significant boost to our programming capabilities.

## 10.2 case classes

The simplest way to start with user defined types in Scala is with case classes. We will start with two examples that were mentioned above: a 3-D point and a student with some grades.

```
case class Point3D(x:Double, y:Double, z:Double)
case class Student(name:String, assignments:List[Double], tests:List[Double], quizzes:List[Double])
```

The first one declares a type called Point3D that stores inside of three Doubles that are named x, y and z. The second declares a type called Student that has a name which is String and different Lists of Double to use as grades.
There can be more to the declaration of a case class, but for now we will limit our syntax to that which begins with the keywords “case class”. After that is the name you want to give the type. This could be any valid Scala name, but it is customary to begin types with uppercase letters and use camel naming so all subsequent words begin with uppercase letters. After that it is a list of name/type pairs in parentheses. The format of these is just like the arguments to a function. The elements of this list give the name and types of the values stored in this new type. The values stored in a class are called MEMBERS and a case class is a class.

> Using a type declaration, it is possible to give a more meaningful name to a tuple, but it is still an equivalent type, so the compiler will accept any tuple of the correct structure and does not help you much finding errors.

### 10.2.1 Making Objects

After you have declared a type, you need to be able to create objects of type. With a case class, you can do this with an expression that has the name of the class followed by an argument, just like a function call. The two classes listed above could be created and stored in variables with the following lines of code.

```
val p = Point3D(1, 2, 3)
val s = Student("Lisa", Nil, Nil, List(89))
```

The first line makes that x=1, y=2, and z=3 stores a reference to it in a variable named p. The next line makes a student with the name "Lisa" who has no assignment or test grades, but has 89 and stores a reference to it in a variable named s. You could insert the word new and a space so that these lines look like.

```
val p = new Point3D(1, 2, 3)
val s = new Student("Lisa", Nil, Nil, List(89))
```

The result of this would be exactly the same. The first syntax is shorter and works for all case classes so we will stick with that.

### 10.2.2 Access Members

In order to be able to use these objects, we must be able to access the different members in them. This is very simple to do, just use the dot notation to access the members. 

```
scala p.x
res1: Double = 1.0
```

To get the name of the Student would do this.

```
scala s.name
res2: String = "Lisa"
```

The dot notation in Scala simply means that you are using a value that is stored inside of an object. It could be a method or a value. For now we will only be concerned with the values we store in case classes. We could use this by writing a function to find the distance between two Point3Ds. It might look like this.

```
def distance(p1:Point3D, p2:Point3D):Double = {
  val dx = p1.x-p2.x
  val dy = p1.y-p2.y
  val dz = p1.z-p2.z
  math.sqrt(dx*dx + dy*dy + dz*dz)
}
```

We could use it to calculate the average for a Student. Note that the minimum grade is thrown out.

> In chapter 6 you will learn that the use of new by default. To get around this requires writing some code also covered in that chapter.

### Introduction to Programming and Problem Solving

One of the things to note about classes is that the members in them are immutable by default. You cannot change what they refer to. If you try to make such a change you get something like the following.

```
scala p.x = 99
error: assignment to val p.x
```

Whether you can change the fields in an object created depends on whether it is mutable or not. In our examples, all of the contents are immutable. As a result, the case class as a whole is immutable and cannot change its value in any way. However, if one or more of the fields in the case class were mutable, then the values in the Array would be. You would not be able to change the size of the Array without making a new object, but you could change the values stored in it.

### 10.2.3 Named and Default Arguments (Advanced)

Normally, arguments are passed into a function by position to the corresponding parameter variables, but Scala figures out which argument is which by their order. Consider this function.

```
def evalQuadratic(a:Double, b:Double, c:Double, x:Double):Double = {
  val x2 = x*x
  a*x2 + b*x + c
}
```

If you load this into the REPL you can execute it as follows.

```
scala> evalQuadratic(a=2, b=3, c=4, x=5)
res3: Double = 69.0
```

In this case, a=2, b=3, c=4, and x=5. This is because the order the arguments appear in both the definition of the function and the call to it. For functions where there are a significant number of arguments that are all of the same type, this can lead to confusion. To get around this, Scala has NAMED ARGUMENTS. When you call the function, you can specify the names you want the values associated with. So the call above would be like the following:

```
scala> evalQuadratic(a=2, b=3, c=4, x=5)
res4: Double = 69.0
```

### Case Classes

In this call it is explicit what values are going to parameters. One advantage is you can enter the arguments in a different order. For example, you might inadvertently think that x was the first argument instead of the last. Without named arguments, this would lead to an error with no error message. You would simply get the wrong answer. If you use named arguments it is fine because names supersede the order.

```
scala evalQuadratic(x=5, a=2, b=3, c=4)
res5: Double = 69.0
```

We see that even though x is first, the value is correct.
You can use named parameters without naming all the parameters. You can start the list with arguments that are based on position and use names for the ones later. All arguments after the first one have to be named, and they cannot duplicate any that you gave using the position.

For some functions, there are arguments that will provide a particular value of that. For example, if you were creating a program to help a local bank calculate loans, it might be likely that most of their customers live in the same state. In that case it is nice to make it so that calling the function does not have to provide a value for the state and let the function use a DEFAULT VALUE. When you declare the function simply follow the type with an equals sign and the value you want for the default. If the caller calls with the default value, then argument can be left out. Default arguments are in the middle then you will have to use named arguments to specify any arguments after them. Consider a function to add a grade to a Student

```
def addGrade(name:String, grade:Int = 0):Student = ...
```

Here the default grade is a zero. This function can be called in two ways.

```
addGrade("Quinn", 95)
addGrade("Kyle")
```

The first call is everything we have to this point. The second one leaves off the grade. As a result, Kyle gets a 0 for whatever grade this was.

### 10.2.4 The copy Method

The fact that you cannot mutate the values in a case class means that it would be helpful to have a way to make new case class objects that are slightly different from existing instances. To see this, consider what happens when you want to add a new grade to a Student. The grades are in Lists, and it is easy to add to a List. The problem is, that does not mutate the original List, it gives you a new List that includes the new values as what was already there.

To help around this problem, case classes come with a copy method. The copy method is intended to be used with the named arguments that were discussed in section 10.2.3. The arguments to copy have the same names as the fields in the class. Using named arguments, you only provide the ones you want to change. Anything you leave out will be copied straight over to the new object.
