
```
23
24     if ( z.compareTo( max ) > 0 )
25         max = z; // z is the largest
26
27     return max; // returns the largest object
28 } // end method maximum
29 } // end class MaximumTest
```

```
Maximum of 3, 4 and 5 is 5
Maximum of 6.6, 8.8 and 7.7 is 8.8
Maximum of pear, apple and orange is pear
```

**Fig. 21.5 | Generic method maximum with an upper bound on its type parameter. (Part 2 of 2.)**

### Generic Method maximum

Generic method maximum (lines 17–28) uses type parameter T as the return type of the method (line 17), as the type of method parameters x, y and z (line 17), and as the type of local variable max (line 19). The type-parameter section specifies that T extends Comparable<T>—only objects of classes that implement interface Comparable<T> can be used with this method. In this case, Comparable is known as the upper bound of the type parameter. By default, Object is the upper bound. Type-parameter declarations that bound the parameter always use keyword extends regardless of whether the type parameter extends a class or implements an interface. This type parameter is more restrictive than the one specified for printArray in Fig. 21.3, which was able to output arrays containing any type of object. The restriction of using Comparable<T> objects is important, because not all objects can be compared. However, Comparable<T> objects are guaranteed to have a compareTo method.

Method maximum uses the same algorithm that we used in Section 6.4 to determine the largest of its three arguments. The method assumes that its first argument (x) is the largest and assigns it to local variable max (line 19). Next, the if statement at lines 21–22 determines whether y is greater than max. The condition invokes y’s compareTo method with the expression y.compareTo(max), which returns a negative integer, 0 or a positive integer, to determine y’s relationship to max. If the return value of the compareTo is greater than 0, then y is greater and is assigned to variable max. Similarly, the if statement at lines 24–25 determines whether z is greater than max. If so, line 25 assigns z to max. Then line 27 returns max to the caller.

### Calling Method maximum

In main (lines 6–14), line 9 calls maximum with the integers 3, 4 and 5. When the compiler encounters this call, it first looks for a maximum method that takes three arguments of type int. There’s no such method, so the compiler looks for a generic method that can be used and finds generic method maximum. However, recall that the arguments to a generic method must be of a reference type. So the compiler autoboxes the three int values as Integer objects and specifies that the three Integer objects will be passed to maximum. Class Integer (package java.lang) implements the Comparable<Integer> interface such that method compareTo compares the int values in two Integer objects. Therefore, Integers are valid arguments to method maximum. When the Integer representing the maximum is returned, we attempt to output it with the %d format specifier, which outputs an int primitive-type value. So maximum’s return value is output as an int value.

A similar process occurs for the three double arguments passed to maximum in line 11. Each double is autoboxed as a Double object and passed to maximum. Again, this is allowed because class Double (package java.lang) implements the Comparable<Double> interface. The Double returned by maximum is output with the format specifier %.1f, which outputs a double primitive-type value. So maximum’s return value is auto-unboxed and output as a double. The call to maximum in line 13 receives three Strings, which are also Comparable<String> objects. We intentionally placed the largest value in a different position in each method call (lines 9, 11 and 13) to show that the generic method always finds the maximum value, regardless of its position in the argument list.

### Upper Bound of a Type Parameter

When the compiler translates method maximum into bytecodes, it uses erasure (introduced in Section 21.3) to replace the type parameters with actual types. In Fig. 21.3, all generic types were replaced with type Object. Actually, all type parameters are replaced with the so-called upper bound of the type parameter, which is specified in the type-parameter section. To indicate the upper bound, follow the type parameter’s name with the keyword extends and the class or interface name that represents the upper bound, or a comma-separated list of the types that represent the upper bound. The list may contain zero or one class and zero or more interfaces. For example, in method maximum’s type-parameter section (Fig. 21.5), we specified the upper bound of the type parameter T as type Comparable<T> as follows:

```
T extends Comparable<T>
```

Thus, only Comparable<T> objects can be passed as arguments to maximum—anything that is not a Comparable<T> will result in compilation errors. Unless specified otherwise, Object is the default upper bound. Figure 21.6 simulates the erasure of method maximum’s types by showing the method’s source code after the type-parameter section is removed and type parameter T is replaced with the upper bound, Comparable, throughout the method declaration. The erasure of Comparable<T> is simply Comparable.

```
1 public static Comparable maximum(Comparable x, Comparable y, Comparable z)
2 {
3     Comparable max = x; // assume x is initially the largest
4
5     if ( y.compareTo( max ) > 0 )
6         max = y; // y is the largest so far
7
8     if ( z.compareTo( max ) > 0 )
9         max = z; // z is the largest
10
11     return max; // returns the largest object
12 } // end method maximum
```

**Fig. 21.6 | Generic method maximum after erasure is performed by the compiler.**

After erasure, method maximum specifies that it returns type Comparable. However, the calling method does not expect to receive a Comparable. It expects to receive an object of the same type that was passed to maximum as an argument—Integer, Double or String in this example. When the compiler replaces the type-parameter information with the upper-bound type in the method declaration, it also inserts explicit cast operations in front of each method call to ensure that the returned value is of the type expected by the caller. Thus, the call to maximum in line 9 (Fig. 21.5) is preceded by an Integer cast, as in

```
(Integer) maximum( 3, 4, 5 )
```

the call to maximum in line 11 is preceded by a Double cast, as in

```
(Double) maximum( 6.6, 8.8, 7.7 )
```

and the call to maximum in line 13 is preceded by a String cast, as in

```
(String) maximum( "pear", "apple", "orange" )
```

In each case, the type of the cast for the return value is inferred from the types of the method arguments in the particular method call, because, according to the method declaration, the return type and the argument types match.

### Possible ClassCastExceptions

In this example, you cannot use a method that accepts Objects, because class Object provides only an equality comparison. Also, without generics, you’d be responsible for implementing the cast operation. Using generics ensures that the inserted cast will never throw a ClassCastException, assuming that generics are used throughout your code (i.e., you do not mix old code with new generic code).

## 21.5 Overloading Generic Methods

A generic method may be overloaded. A class can provide two or more generic methods that specify the same method name but different method parameters. For example, generic method printArray of Fig. 21.3 could be overloaded with another printArray generic method with the additional parameters lowSubscript and highSubscript to specify the portion of the array to output (see Exercise 21.5).

A generic method can also be overloaded by nongeneric methods. When the compiler encounters a method call, it searches for the method declaration that most precisely matches the method name and the argument types specified in the call. For example, generic method printArray of Fig. 21.3 could be overloaded with a version that’s specific to Strings, which outputs the Strings in neat, tabular format (see Exercise 21.6).

When the compiler encounters a method call, it performs a matching process to determine which method to invoke. The compiler tries to find and use a precise match in which the method name and argument types of the method call match those of a specific method declaration. If there’s no such method, the compiler attempts to find a method with compatible types or a matching generic method.

## 21.6 Generic Classes

The concept of a data structure, such as a stack, can be understood independently of the element type it manipulates. Generic classes provide a means for describing the concept of a stack (or any other class) in a type-independent manner. We can then instantiate type-specific objects of the generic class. This capability provides a wonderful opportunity for software reusability.
