# Exercises

21.3 (Explain Notation) Explain the use of the following notation in a Java program:

```
public class Array< T > { }
```

21.4 (Generic Method selectionSort) Write a generic method selectionSort based on the sort program of Figs. 19.6–19.7. Write a test program that inputs, sorts and outputs an Integer array and a Float array. [Hint: Use <T extends Comparable<T> > in the type-parameter section for method selectionSort, so that you can use method compareTo to compare the objects of the type that T represents.]

21.5 (Overloaded Generic Method printArray) Overload generic method printArray of Fig. 21.3 so that it takes two additional integer arguments, lowSubscript and highSubscript. A call to this method prints only the designated portion of the array. Validate lowSubscript and highSubscript. If either is out of range, the overloaded printArray method should throw an InvalidSubscriptException; otherwise, printArray should return the number of elements printed. Then modify main to exercise both versions of printArray on arrays integerArray, doubleArray and characterArray. Test all capabilities of both versions of printArray.

21.6 (Overloading a Generic Method with a Nongeneric Method) Overload generic method printArray of Fig. 21.3 with a nongeneric version that specifically prints an array of Strings in neat, tabular format, as shown in the sample output that follows:

```
Array stringArray contains:
one    two    three    four
five   six    seven    eight
```

21.7 (Generic isEqualTo Method) Write a simple generic version of method isEqualTo that compares its two arguments with the equals method and returns true if they’re equal and false otherwise. Use this generic method in a program that calls isEqualTo with a variety of built-in types, such as Object or Integer. What result do you get when you attempt to run this program?

21.8 (Generic Class Pair) Write a generic class Pair which has two type parameters—F and S—each representing the type of the first and second element of the pair, respectively. Add get and set methods for the first and second elements of the pair. [Hint: The class header should be public class Pair<F, S>.]

21.9 (Overloading Generic Methods) How can generic methods be overloaded?

21.10 (Overload Resolution) The compiler performs a matching process to determine which method to call when a method is invoked. Under what circumstances does an attempt to make a match result in a compile-time error?

21.11 (What Does this Statement Do?) Explain why a Java program might use the statement

```
ArrayList< Employee > workerList = new ArrayList< Employee >();
```