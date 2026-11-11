If you like, you can pass the object to a method:

```
System.out.println(new Date());
```

Alternatively, you can apply a method to the object that you just constructed. One of the methods of the Date class is the toString method. That method yields a string representation of the date. Here is how you would apply the toString method to a newly constructed Date object:

```
String s = new Date().toString();
```

In these two examples, the constructed object is used only once. Usually you will want to hang on to the objects that you construct so that you can keep using them. Simply store the object in a variable:

```
Date birthday = new Date();
```

Figure 4.3 shows the object variable birthday that refers to the newly constructed object.

![](bbox=[0.236, 0.469, 0.678, 0.631])

**Figure 4.3** Creating a new object

There is an important difference between objects and object variables. For example, the statement

```
Date deadline; // deadline doesn't refer to any object
```

defines an object variable, deadline, that can refer to objects of type Date. It is important to realize that the variable deadline is not an object and, in fact, does not even refer to an object yet. You cannot use any methods on this variable at this time. The statement

```
s = deadline.toString(); // not yet
```

would cause a compile-time error.