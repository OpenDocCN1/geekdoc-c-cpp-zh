
- You cannot change operator precedence.
- You cannot change the arity of an operator.
  - no postfix !
  - no binary ~
  - no unary ^
- You cannot define a new action for an intrinsic operator for a native C++ data type. That is, you cannot change the way the + operator works on two `int`s.
- Overloaded operators may not have default arguments.

To overload an operator, you define a function for the compiler to call when that operator is used with the appropriate data types. Whenever the compiler sees those data types used with the operator, it calls the function.

## Overloading Unary Operators

Let's start off by overloading a unary operator. Unary operators act on only one operand (++, --, -).

We'll look at the Counter class we previously defined. Objects of that class were incremented by calling a member function:

```
c1.incCount();
```

That did the job, but the listing would have been more readable if we could have used the increment operator ++ and simply said:

```
++c1;
```

Here's our newest version of the Counter class, rewritten to use an overloaded increment operator:

```
class Counter {
   private:
      int count;
   public:
      Counter() { count = 0; }
      int getCount() { return count; }
      void operator++() { ++count; }
};

int main() {
   Counter c1, c2;
   cout << "c1 = " << c1.getCount() << endl;
   cout << "c2 = " << c2.getCount() << endl;
   ++c1;
   ++c2;
   cout << "c1 = " << c1.getCount() << endl;
   cout << "c2 = " << c2.getCount() << endl;
   return 0;
}
```

The keyword `operator` is used to overload the `++` operator in the class. The overloaded `++` operator function is made up of four components:

- return type: void
- keyword operator: operator
- operator to be overloaded: ++
- argument list in parentheses: ()

The compiler calls this member function whenever the `++` operator is encountered, provided the operand is of type `Counter`.

Note: as seen before, the compiler distinguishes between overloaded functions by the type and number of their arguments. Similarly, the compiler distinguishes between overloaded operators by the types of their operands.

In `main()`, the `++` operator is applied to a specific object as shown. Yet, `operator++()` takes no arguments. So what does this operator increment? It increments the count data member in the object `c1`, the object which used the operator `++`. Since member functions can always access the particular object for which they've been called, this operator requires no arguments.

The `operator++()` function has a subtle defect which you'll see if you try to execute this statement:

```
c1 = ++c2;
```

The compiler will complain. Why?

We've defined the `++` operator to have a return type of `void` in the `operator++()` function. But in the statement:

```
c1 = ++c2;
```

the function is asked to return a value of type `Counter`. The compiler is being asked to return whatever value `c2` has after being operated on by the `++` operator, and then assign this value to `c1`. So we can't use our `++` operator to increment `Counter` objects in expressions.

To make it possible to use our `operator++()` in expressions, we must provide a way for it to return a value:

```
class Counter {
   private:
      int count;
   public:
      Counter()
         { count = 0; }
      int getCount()
         { return count; }
      Counter operator++()
      {
         ++count;
         Counter temp;
         temp.count = count;
         return temp;
      }
};
```

In this version of the class, our `operator++()` function returns a value of class Counter.

- it increments the count data in its own object as before.
- the function creates a new object of type `Counter`, called `temp`, to use as a return value
- it assigns `count` in the temporary object the same value as in itself
- it returns the `temp` object

These changes now allow for the following style of expression in `main()`:

```
c2 = ++c1;       // displays itself using the
++c1.getCount()   // getCount() member function.
```

There are more convenient ways to return objects from functions and overloaded operators. Previously, we created a temporary object to return a function value that took three lines of code. We can actually do it with a simple statement:

```
Counter operator++() {
	++count;
	return Counter(count);
}
```

This code:

- creates an object of type Counter that has no name (it won't be around long enough to need one)

- this unnamed object is initialized to the value provided by the argument count.

- C++ treats this as a constructor call for a temporary object with no name and a very brief lifetime. However, the code does require a constructor that takes one argument:

```
Counter(int c) { count = c; }
```

- Once the unnamed object is initialized to the value of count, it can then be returned

We can do the same with decrement operators:

```
Counter operator--() {
	--count;
	return Counter(count);	// or return *this;
}
```

## Distinguishing Prefix and Postfix for ++ and -- Operators

In earlier versions of C++, it was impossible to define separate overloaded operations for postfix and prefix ++ and -- operators. However, the compiler can now distinguish between the prefix and postfix versions of these operators by calling the operator function prefix with no arguments or with one int argument, respectively.

```
class Counter {
   private:
      int count;
   public:
      Counter() { count = 0; }
      Counter(int x) { count = x; }
      int getCount() { return count; }
      Counter operator++() {
         ++count;
         return Counter(count); // or return *this;
      }
      Counter operator++(int) {
         int temp = count;
         ++count;
         return Counter(temp);
      }
};
```

Member functions operator++(int) and operator--(int) defines a postfix increment and decrement operator for a Counter object. C++ assigns 0 to the single int parameter.

For an object c1 of type Counter, the expression ++c1 calls the overloaded prefix ++ operator, in effect executing the statement:

```
c1.operator++();
```

The expression c1++ calls the overloaded postfix ++ operator and executes as though written:

```
c1.operator++(0);
```

The decrement operator works similarly.

Because older versions of C++ did not make the distinction between prefix and postfix, some newer compilers might allow both calls to be made with only the prefix definition of `operator++()` or `operator--()`, although they usually issue a warning.

Notice that the argument `int` has no identifier, so it is not used in the function. It is only there to generate a different function signature. Because there is no identifier, the compiler will not complain that a variable has been “created but not used”.

Our main concern when creating prefix and postfix operators is to decide what incrementing and decrementing means for an object of this class. In most cases, there’s a specific data member in the class that you’ll want to increment or decrement.

## Overloading Binary Operators

Our previous Distance class was defined as follows:

```
class Distance {
private:
    int feet;
    float inches;
public:
    Distance() { } // default constructor
    Distance(int ft, float in) { feet = ft; inches = in; }
};

void Distance::addDist(Distance d2, Distance d3) {
    feet = d2.feet + d3.feet;
    inches = d2.inches + d3.inches;
    if (inches >= 12.0) {
        inches -= 12.0;
        ++feet;
    }
}
```

Using this Distance class, we would add two Distance objects as:

```
d3.addDist(d1, d2);
```

We will now overload the + operator to perform the addition of two Distance objects as:

```
d3 = d1 + d2;
```

We can now rewrite the class as:

```
class Distance {
private:
	int feet;
	float inches;
public:
	Distance() {} // default constructor
	Distance(int ft, float in) { feet = ft; inches = in; }
	Distance operator+(Distance d);
};

Distance Distance::operator+(Distance d) {
	int ft = feet + d.feet;
	float inches = inches + d.inches;
	if (inches >= 12.0) {
		inches -= 12.0;
		++ft;
	}
	return Distance(ft, in);
}
```

When the compiler sees an expression like:

```
d3 = d1 + d2;
```

it realizes it must use the `Distance` member function `operator+()`. But what does this function use as its argument, `d1` or `d2`? And why doesn't it need two arguments, since two numbers are added?

The argument on the left side of the operator, `d1`, is the object that really calls the operator member function. The object on the right side of the operator, `d2`, must be furnished as an argument to the operator.

In the `operator+()` function, data members left of the operand are accessed directly as feet and inches, since this is the object which really called the member function. The right operand is accessed as the function's argument, as `d2.feet` and `d2.inches`.

Note: Overloaded operators always require one less argument than the number of operands. This is true since one operand is the object that called the member function. That is also why unary operators require no arguments.
