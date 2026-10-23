
# 10.2.1 Making Objects

After you have declared a type, you need to be able to create objects of that type. With a **case** class, you can do this with an expression that has the name of the class followed by an argument list, just like a function call. The two classes listed above could be created and stored in variables with the following lines of code.

```
val p = Point3D(1,2,3)
val s = Student("Mark",Nil,Nil,List(89))
```

The first line makes a point that has x=1, y=2, and z=3 and stores a reference to it in a variable named p. The next line makes a student with the name "Mark" who has no assignment or test grades, but who has an 89 on one test and stores a reference to it in a variable named s.

You could insert the word **new** and a space after the equals signs so that these lines look like the following.

```
val p = new Point3D(1,2,3)
val s = new Student("Mark",Nil,Nil,List(89))
```

The result of this would be exactly the same. The first syntax is shorter and works for all case classes so we will stick with that in our sample code.¹

# 10.2.2 Accessing Elements

In order to be able to use these objects, we must be able to access the different elements in them. This is very simple to do, just use the dot notation to access the elements. So if you want the x value in the Point3D, p that we made above, you would just do this.

```
scala> p.x
res1: Double = 1.0
```

To get the name of the Student you would do this.

```
scala> s.name
res2: String = Mark
```

The dot notation in Scala simply means that you are using something from inside of an object. It could be a method or a value that is stored in the object. For now we will only be concerning ourselves with the values that we store in our case classes.

We could put this to use by writing a function to find the distance between two Point3Ds. It might look something like this.

```
def distance(p1:Point3D,p2:Point3D):Double = {
  val dx=p1.x-p2.x
  val dy=p1.y-p2.y
  val dz=p1.z-p2.z
  math.sqrt(dx*dx+dy*dy+dz*dz)
}
```

We could also use it to calculate and average for a Student with code like this.

```
def classAverage(s:Student):Double = {
```

¹In chapter 16 you will learn that normal classes require the use of new by default. To get around this requires writing some code in a companion object, a technique also covered in that chapter.

```
val assnAve=if(s.assignments.isEmpty) 0.0
  else s.assignments.sum/s.assignments.length
val quizAve=if(s.quizzes.length<2) 0.0
  else (s.quizzes.sum-s.quizzes.min)/(s.quizzes.length-1)
val testAve=if(s.tests.isEmpty) 0.0
  else s.tests.sum/s.tests.length
0.5*assnAve+0.3*testAve+0.2*quizAve
}
```

The if expressions here prevent us from doing division by zero.

One of the things to note about case classes is that the elements in them are vals. As such, you can not change what they refer to. If you try to make such a change you get something like the following.

```
scala> p.x=99
<console>:8: error: reassignment to val
    p.x=99
```

Whether you can change anything in an object created from a case class depends on whether the things in it are mutable or not. In our two examples, all of the contents are immutable. As a result, the case class as a whole is immutable. Once you create a Point3D or a Student, the object you create can not change its value in any way. However, if one or more of the fields in the case class were an Array, then the values in the Array would be mutable. You would not be able to change the size of the Array without making a new object, but you could change the values stored in it.

# 10.2.3 Named and Default Arguments (Advanced)

A few options were added to Scala in version 2.8 in regards to function arguments and calling functions. Normally, Scala figures out which of the arguments passed into a function is associated with which formal parameter by their order. Consider this function.

```
def evalQuadratic(a:Double,b:Double,c:Double,x:Double):Double = {
  val x2=x*x
  a*x2+b*x+c
}
```

If you load this into the REPL you can execute it as follows.

```
scala> evalQuadratic(2,3,4,5)
res0: Double = 69.0
```

In this call, a=2, b=3, c=4, and x=5. This is because that is they order the arguments to appear in both the definition of the function and the call to it. For functions where there are a significant number of arguments that are all of the same type, this can lead to confusion. To get around this, Scala has NAMED ARGUMENTS. When you call the function you can specify the names you want the values associated with it. So the call above would be like the following:

```
scala> evalQuadratic(a=2,b=3,c=4,x=5)
```

```
res2: Double = 69.0
```

In this call it is now explicit what values are going to what parameters. One advantage of this is when you enter the arguments in a different order, the meaning will be what you want. For example, you might think that x was the first argument instead of the last. Without names arguments, this would lead to an error with no error message. You would simply get the wrong answer. However, if you use named arguments everything is fine because the names supersede the order.

```
scala> evalQuadratic(x=5,a=2,b=3,c=4)
res3: Double = 69.0
```

Here we see that even though x is first, the value we get is correct.

You can use named parameters without naming all the parameters. You can start the list with arguments that are based on position and then use names for the later ones. All the arguments after the first named one have to be named and they can not duplicate any that you gave using the position.

For some functions there are some arguments that will have a particular value a lot of the time. In that situation, it is nice to make it so that people calling the function do not have to provide them and they will use a DEFAULT VALUE. When you declare the function simply follow the type with an equals sign and the value you want to have for the default. If the caller is happy with the default value, then that argument can be left out. Default arguments at the end of the list can be simply omitted. If they are in the middle then you will have to use named arguments to specify any arguments after them in the list. Consider a function to add a grade to a Student.

```
def addGrade(name:String,grade:Int = 0):Student = ...
```

Here the default grade is a zero. So this function can be called in two ways.

```
addGrade("Jane",95)
addGrade("Joe")
```

The first call is like everything we have seen to this point. The second one leaves off the grade. As a result, Joe gets a 0 for whatever grade this was.

# 10.2.4 The copy Method

The fact that you can not mutate the values in a case class means that it would be helpful to have a way to make new case class objects that are only slightly changed from others. To see this, consider what happens when you want to add a new grade to a Student. The grades are in Lists, and it is easy to add to a List. The problem is, that does not mutate what is in the original List, it just gives us a new List that includes the new values as well as what was already there.

To help get around this problem, case classes come with a copy method. The copy method is intended to be used with the named arguments that were discussed in section 10.2.3. The arguments to copy have the same names as the fields in the class. Using named arguments, you only provide the ones you want to change. Anything you leave out will be copied straight over to the new object. So using the Student object we gave the name s above, we could use copy to do the following.

```
val ns = s.copy(tests = 99::s.tests)
```

This gives us back a new **Student** who is the same as the one we had in s, only it has a test grade of 99 in addition to the quiz grade of 89 it had originally.

You can specify as many or as few of the fields in the **case class** as you want. Whatever fields you give the names of will be changed to the value that you specify. If you leave the parentheses empty, you will simply get a copy of the object you have originally.

# 10.2.5 Case Class Patterns

Another capability that comes with **case classes** is that you can use them in patterns. This can be used as a simple way to pull values out of an instance or to select between objects in a match. As an example of pulling out values, consider the following code using Point3D.

```
for(Point3D(x,y,z) <- points) {
// Do stuff with x, y, and z.
}
```

This is a **for** loop that runs through a collection of points. Instead of calling each point with a name like point, this pulls out the values in the point and gives them the names x, y, and z. That can make things shorter and more clear in the body of the loop.

As an example of limiting what is considered, we can use another **for** loop that goes through a course full of students.

```
for(Student(name,_,List(t1,t2,t3),_) <- courseStudents) {
// Processing on the students with three test grades.
}
```

This does something with patterns that we have not seen before; it nests them. You can nest patterns in any way that you want. This is part of what makes them extremely powerful. In this case, the assignment and quiz grades have been ignored and the loop is limited to only considering students with exactly three test grades. Those grades are given the names t1, t2, and t3. That could also have been specified with the pattern t1::t2::t3::Nil. Students who have more or fewer test grades will be skipped over by this loop.

# 10.3 Mutable Classes

**case classes** are not the only option you have when creating **classes**. We will go into the full details of **classes** in chapter 16. There are some applications for which you do not need the full power classes can provide, but you would like to have fields in the class that are mutable. Remember that every field in a case class is like a val so the case class is generally immutable. The only way the value of something in a case class can change is if one of the fields references a mutable value like an **Array**.

When you want to make objects with mutable fields, you need to leave off the **case** keyword and just define a **class**. To be able to use the fields, given what you currently know, each one will need to be preceded by either val or var. If you put val before a field its value will not be allowed to change. If you use var, the field will be allowed to change. So if you have objects that truly need to be altered because they change very rapidly and
