The System namespace defines a set of delegates, and the delegate Func<T, bool> represents a method that takes one parameter of a generic type T and returns a Boolean value. In all Func<...> style delegates, the last type is the return type.

The List<T>.Contains(T item) method returns true if the item is in the list or false otherwise. Again, ushort[] is a subtype of List<ushort>. The Count() method goes through all elements in the whites array, and it counts those that are contained in the numbers array. Hence, the method call whites.Count(numbers.Contains) ends up returning the number of balls that are both in the whites and numbers arrays.

The method like Count<T>(...) is often known as the "higher order function" because it is a function (method in C#) that take a function argument (delegate in C#).

> The System.Linq namespace includes a set of commonly used methods that are higher order functions. We will not go through all these methods in this book, but the readers are encouraged to consult other references. For example, refer to the Microsoft doc for a list of (extension) methods defined on the IEnumerable<T> Class [https://docs.microsoft.com/en-us/dotnet/api/system.linq.enumerable?view=net-5.0].

The System.Random class represents a pseudo-random number generator, which is an algorithm that produces a sequence of numbers that meet certain statistical requirements for randomness.

The Random class defines a number of different methods to get random int, byte, or real numbers. The static Game.DrawBalls() method uses the Random.Next(int) instance method to get a non-negative random integer that is less than the specified maximum. That is, in this particular case, rand.Next(25), for example, will return a random integer between 0 (inclusive) and 25 (exclusive). (25 possible values in total.)

Note that we add the number 1 to make the numbers fall within the range of 1 and