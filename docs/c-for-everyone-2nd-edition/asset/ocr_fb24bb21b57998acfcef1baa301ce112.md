> You can drive a car by operating the steering wheel and pedals, without knowing how the engine works. Similarly, you use an object through its member functions. The implementation is hidden.

![](bbox=[0.381, 0.102, 0.851, 0.348])

When you develop an object-oriented program, you create your own classes that describe what is important in your application. For example, in a student database you might work with Student and Course classes. Of course, then you must supply member functions for these classes.

When you work with an object, you do not know how it is implemented. You need not know how a string organizes a character sequence, or how the cin object reads input from the console. All you need to know is the public interface: the specifications for the member functions that you can invoke. The process of providing a public interface, while hiding the implementation details, is called encapsulation.

> Every class has a public interface: a collection of member functions through which the objects of the class can be manipulated.

> Encapsulation is the act of providing a public interface and hiding implementation details.

You will want to use encapsulation for your own classes. When you define a class, you will specify the behavior of the public member functions, but you will hide the implementation details. Encapsulation benefits the programmers who use your classes. They can put your classes to work without having to know their implementations, just as you are able to make use of the string and stream classes without knowing their internal details.

> Encapsulation enables changes in the implementation without affecting users of a class.

Encapsulation is also a benefit for the implementor of a class. When working on a program that is being developed over a long period of time, it is common for implementation details to change, usually to make objects more efficient or more capable. Encapsulation is crucial to enabling these changes. When the implementation is hidden, the implementor is free to make improvements. Because the implementation is hidden, these improvements do not affect the programmers who use the objects.

> A driver of an electric car doesn't have to learn new controls even though the car engine is very different. Neither does the programmer who uses an object with an improved implementation—as long as the same member functions are used.

![](bbox=[0.633, 0.734, 0.924, 0.906])