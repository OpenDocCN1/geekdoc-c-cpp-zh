
# Object Oriented Programming using C# Generic Collections and how to Serialize them

In these cases respectively the CLR engine will treat int, double, and Student objects as the most general type of thing available 'Object'. It will then convert this object to a string and compare the strings.

This will work however in many situations creating methods which take parameters of type 'Object' is flawed or at least very limited.

Inside these methods we do not know what type of object was actually passed as a parameter and hence in the example above we do not know what type of object is actually being returned. When two students object are passed the object returned is a student but we cannot invoke Student-specific methods on this object unless we first cast the object returned to a Student.

![](img/e143b38d00f95425fa4f3efca0527189_130_0.png)

# Object Oriented Programming C# Generic Collections and how to Serialize them

Assume that we want to invoke an 'AwardMerit()' method on the 'Student' returned via the Highest() method. We can do this if we first cast the 'Object' onto a 'Student' object. E.g.

```
(Student)Highest(studentA, studentB).AwardMerit();
```

However the compiler cannot be certain that the returned object is a 'Student' and the compiler cannot detect the potentially critical error that would occur if we invoked Highest() on two integers and then tried to cast the returning integer onto an object of 'Student'.

This leads to the idea that we would like to be create a method that will take parameters of ANY type and return values that are again of ANY type but where we define these types when we invoke these methods. Such methods exist and they are called Generic Methods.

Generic methods are methods where the parameter types are not defined until the method is invoked. Parameter types are specified each time the method is invoked and the compiler can still check the code is valid.

In other ways a generic method uses a – data type that is determined by a parameter.

In the code below a generic method Highest() has been defined as a method that takes two objects as parameters of unspecified type -

```
public T Highest<T>(T o1, T o2)
{
    if (o1.ToString().compareTo(o2.ToString()) > 0)
        return o1;
    else
        return o2;
}
```

We can use this method and each time we invoke it we define the type of object being compared. If two students compared the compiler will know that the object returned is also type student and will therefore know it is legal to invoke specific methods on this object.

A list of generic data types contained between angle brackets that follow the method's name is provided. If multiple generic types are used by a method, their names are separated by commas.

In the example above, the identifier T can stand for any data type. So, when T is used within the brackets in the method's parameter list to describe data, it might be an int, 'Student' or any other data type. The only requirement is that the method must work no matter what type of object is passed to it. All objects have a ToString() method because every data type inherits the ToString() method from the 'Object' class, or contains its overriding version.

# Object Oriented Programming C#

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

The generic data type identifier for a generic method can be any legal C# identifier, but by convention it is usually an upper case letter. "T" is used for "type".

When a generic method is defined i.e. one works with any data type it is specified when the method is used. Thus in the code below, Highest() is a generic method, the compiler can see that a 'Student' object is being passed as a parameter and thus the object being returned must also be of type 'Student'.

```
Student s1 = new Student("Student A");
Student s2 = new Student("Student B");
Student highestStudent = Highest(s1, s2);
```

The object being returned is of type 'Student' it must be OK to store this in a variable of type Student and it must be OK to invoke and Student methods on the object returned.

Generic methods can therefore work with any data type but the compiler can still check for type errors (as the type is specified each time the method is invoked).

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

Generic data type identifier for a generic method can be any legal C# identifier, but by convention it is usually an upper case letter. "T" is used for "type".

When a generic method is defined i.e. one works with any data type it is specified when the method is used. Thus in the code below, Highest() is a generic method, the compiler can see that a 'Student' object is being passed as a parameter and thus the object being returned must also be of type 'Student'.

```
Student s1 = new Student("Student A");
Student s2 = new Student("Student B");
Student highestStudent = Highest(s1, s2);
```

The object being returned is of type 'Student' it must be OK to store this in a variable of type Student and it must be OK to invoke and Student methods on the object returned.

Generic methods can therefore work with any data type but the compiler can still check for type errors (as the type is specified each time the method is invoked).

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

## 7.2 Introduction to Collections

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful. case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful. case below one generic data type is specified. This is used to define the type of both parameters and the return value.

## 7.3 Types of Collections

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

## 7.4 Lists

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful. case below one generic data type is specified. This is used to define the type of both parameters and the return value.

## 7.5 HashSets

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful. case below one generic data type is specified. This is used to define the type of both parameters and the return value.
