
`class Rectangle;`

are a promise to the compiler that we will declare the classes eventually. The compiler will then allow them to be used as parameter and return types. However, it is not possible to use a class as a member variable or as a superclass until it has been fully declared.

This raises the question of what is the right order in which to put all your declarations, definitions, and so forth within a `C++` file. Here are my recommendations. You should write `cpp` files in the following order.

1.  Include statements.
2.  `using namespace` statements.
3.  Forward declarations of classes.
4.  Class declarations and function declarations.
5.  Function definitions and member definitions.
6.  Tests (other projects often have different test conventions).

## 12.8 The static keyword

Sometimes you may want to associate a function with a class but not with a particular instance. Here are some reasons why you might want to do this.

-   The function is designed to construct instances—a so called *factory method*. We will see a detailed example of this in the next chapter.
-   The function operates on vectors of instances, so you can’t sensibly associate it with a particular instance.
-   The function is designed to change the behaviour of every instance at once. For example, you might want to enable extra logging information for a class to help with debugging.
-   The function is designed to manage all the of instances of your class. For example, since connecting to a database the first time is slow, you might want to maintain a pool of ten connections to a given database. You could then associate functions with the `DatabaseConnection` class that allows you to obtain and return connections from this pool.

If you want to associate a function with the class, but not with any instance, you should use the keyword `static`. You can also declare that a member variable is `static`, which means that it is shared by all instances of the class.

As a somewhat contrived example, let us suppose that we have found a performance problem in our code. We suspect it is something to do with the `evaluate` function of a class we have written to compute the `sin` function. As part of debugging this we want to count just how often this method is called. Here is one way we could do this:

```c++
class CallCountedSin : public RealFunction {
public:
    static int getNumberOfCalls();
    double evaluate(double x) {
        numCalls++;
        return sin(x);
    }
private:
    static int numCalls;
};
```

Our class `CallCountedSin` acts like the `sin` function, but also counts the number of times `evaluate` is called on `any` instance. We have a `static` member variable to save the number of calls and a `static` member function to read the value.

The definition of the function looks just like an ordinary member function.

```c++
int CallCountedSin::getNumberOfCalls() {
    return numCalls;
}
```

Notice that this function is not allowed to access any variables other than those that are `static`.

Here is how we initialize the static variable `numCalls`:

```c++
int CallCountedSin::numCalls = 0;
```

This looks pretty much like a global variable definition. In a sense, that is exactly what it is. The difference is that we have associated the variable `numCalls` with the class `CallCountedSin`. This is an improvement over having a global variable called `numCalls` because the static variable can be declared private. This means it is impossible for it to be used by any function in another class.

Here is an example of how you actually call a static function:

```c++
void testCallCountedSin() {
    CallCountedSin instance1;
    CallCountedSin instance2;
    integral(instance1, 0, 1, 1000);
    integral(instance2, 0, 1, 1000);
    int numCalls=CallCountedSin::getNumberOfCalls();
    ASSERT(numCalls == 2000);
}
```

The point to observe is that to call the function we have to qualify its name with the name of the class.

```c++
int numCalls=CallCountedSin::getNumberOfCalls();
```

Since we could have many classes with identically named static methods, it makes sense that we have to qualify the name.

We have seen an example of a static variable before in Section 9.3. You may recall that we reset the seed of the random number generator using the following code:

```c++
mersenneTwister.seed(mt19937::default_seed);
```

This code is accessing the static variable default_seed that is defined in the class mt19937. Because the default_seed will be the same for all instances, it is logical to associate it with the class rather than any instance. For more complex data objects than a single integer, it may save a considerable amount of memory to have only one copy of a variable that is shared by all instances.

In summary, static functions and static variables behave exactly like global functions and global variables except for the following.

-   They can be made private and have privileged access to private data. This increases encapsulation.
-   They are associated with the class. Calls to static functions need to be qualified with the class name. This prevents name clashes.

Confusingly, C++ also uses the static keyword with functions that aren’t defined in any class. In this context static means “cannot be used outside the current file”. It is unfortunate that C++ uses the same keyword for two completely different purposes.

## Danger!

Just as with other global variables, if you are using multi-threaded code then you must be careful to use locks using non-constant static variables. See Chapter 20.

## 12.9 The protected keyword

We know already that we can use the keywords public or private for information hiding. public means everyone can use the methods and variables. private means nobody can use the methods/variables including subclasses.

Now that we are using sub-classes it is worth saying that you can also use the keyword **protected**. This means only subclasses can use the methods/variables. In practice I recommend ignoring **protected** for the time being as it isn't particularly useful.

### Exercises

1.  12.9.1. Write **DigitalCallOption** and **DigitalPutOption** classes. Refactor **PutOption** so it extends **PathIndependentOption**.
2.  12.9.2. Write an **AsianOption** which represents an Asian option. Show where this new class fits into the UML diagram of options.
3.  12.9.3. Create a UML diagram for the class hierarchy with base class **Shape**.
4.  12.9.4. There is a lot of identical code between our different chart classes. In particular they all have in common a title and two functions called **writeAsHTML**. Design a base class and extend it for each chart. Draw a UML diagram of the resulting hierarchy. Use getter and setter methods to access the title.
5.  12.9.5. Can you use the techniques of this chapter to improve the **Cipher** classes written for Exercise 10.6.6?
6.  12.9.6. This exercise tests the use of static variables and functions.
    1.  Write an interface class **RandomNumberGenerator** that has a function to generate a uniformly distributed random number.
    2.  Write an implementation of **RandomNumberGenerator** that uses the **mt19937** class. This design pattern of implementing an interface by simply calling another class to do all the work is called *delegation*.
    3.  Write a static function on the **RandomNumberGenerator** class called **setDefault** that sets the current default **RandomNumberGenerator** instance. Note that you should use a **shared_ptr<RandomNumberGenerator>** as the parameter to **setDefault**.
    4.  Write a static function **randUniform** on **RandomNumberGenerator** that allows the user to generate a uniformly distributed random number without needing to create a **RandomNumberGenerator**.
    5.  Add a non-static **setDefault** function to **RandomNumberGenerator** that sets the current random number generator to be used as the default random number generator. You will need to use the **this** keyword.
    6.  In what ways, if any, do you think this improves upon the existing functions in **matlib**?
