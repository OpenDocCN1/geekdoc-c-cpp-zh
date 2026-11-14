written during the execution. The functions could have additional printouts for debugging (a debugger is usually a better alternative than putting printouts into programs). We could even allow reading only at certain times of the day or writing only when the program runs on a computer with a certain IP. We will most likely not do the latter, at least not for complex numbers, but we could. If the variables are public and accessed directly, such behavior would not be possible. Nevertheless, handling the real and imaginary parts of a complex number in this fashion is cumbersome and we will discuss better alternatives.

Most C++ programmers would not implement it this way. What would a C++ programmer then do first? Write constructors.

# ## 2.3 Setting Values: Constructors and Assignments

Construction and assignment are two mechanisms to set the value of an object, either at its creation or later. Therefore, these two mechanisms have much in common and are introduced here together.

# ### 2.3.1 Constructors

Constructors are methods that initialize objects of classes and create a working environment for member functions. Sometimes such an environment includes resources like files, memory, or locks that have to be freed after their use. We come back to this later.

Our first constructor will set the real and imaginary values of our complex:

```
class complex
{
public:
	complex(double rnew, double inew)
	{
		r = rnew; i = inew;
	}
	// ...
};
```

A constructor is a member function with the same name as the class itself. It can possess an arbitrary number of arguments. This constructor allows us to set the values of c1 directly in the definition:

```
complex c1(2.0, 3.0);
```

There is a special syntax for setting member variables and constants in constructors called Member Initialization List or for short Initialization List:

```
class complex
{
public:
	complex(double rnew, double inew) : r(rnew), i(inew) { }
	// ...
};
```