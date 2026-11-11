Or you can set the variable to refer to an existing object:

```
```
startTime = rightNow;
```
```

Now both variables refer to the *same* object (see Figure 4.4).

![](bbox=[0.212, 0.236, 0.784, 0.442])

**Figure 4.4** Object variables that refer to the same object

It is important to realize that an object variable doesn’t actually contain an object. It only *refers* to an object.

In Java, the value of any object variable is a reference to an object that is stored elsewhere. The return value of the `new` operator is also a reference. A statement such as

```
```
Date startTime = new Date();
```
```

has two parts. The expression `new Date()` makes an object of type `Date`, and its value is a reference to that newly created object. That reference is then stored in the `startTime` variable.

You can explicitly set an object variable to `null` to indicate that it currently refers to no object.