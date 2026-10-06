width instance variable; it's private and therefore not accessible by the Square class. However, the getter method is inherited from the parent class and can be used to access the value of the width. You'll recall that writing the expression

```
self.width
```

is equivalent to writing

```
[self width]
```

This sends the width message to the receiver of the side message. In other words, you execute the getter method width as opposed to trying to directly access the instance variable width (which, as discussed, you can't do). This is an important concept that you need to understand.

A square has only one side, but you're internally representing it as two numbers—that's all. All that is hidden from the user of the Square class. You can always redefine the Square class later, if necessary; any users of the class don't have to be concerned with the internal details because of the notion of data encapsulation discussed earlier.

The setSide: method takes advantage of the fact that you already have a method inherited from your Rectangle class to set the values of the width and height of a rectangle. So setSide: calls the setColor:andHeight: method from the Rectangle class, passing the parameter s as the value for both the width and height. You don't have to do anything else. Someone working with a Square object can now set the dimensions of the square by using setSide: and can take advantage of the methods from the Rectangle class to calculate the square's area, perimeter, and so on. Program 8.3 shows the test program and output for your new Square class.