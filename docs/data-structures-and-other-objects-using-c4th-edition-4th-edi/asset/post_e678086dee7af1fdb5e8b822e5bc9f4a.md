
The first improvement deals with initializing a throttle. Three of the member functions have a precondition indicating that “shut_off has been called at least once to initialize the throttle.” Without this precondition, the member variable position would contain garbage, and anything might happen. Unfortunately, there is no way to test the precondition to ensure that a throttle has been initialized.

Constructors are a way to solve this problem by providing an initialization function that is guaranteed to be called. A constructor is a member function with these special properties:

- If a class has a constructor, then a constructor is called automatically whenever a variable of the class is declared. If a constructor has any parameters, then the arguments for the constructor call must be given after the variable name (at the point where the variable is declared).
- The name of a constructor must be the same as the name of the class. In our example, the name of the constructor is throttle. This seems strange: Normally we avoid using the same name for two different things. But it is a requirement of C++ that the constructor use the same name as the class.
- A constructor does not have any return value. Because of this, you must not write void (or any other return type) at the front of the constructor’s head. The compiler knows that every constructor has no return value, but a compiler error occurs if you actually write void at the front of the constructor’s head.

## The Throttle's Constructor

Let's make these features concrete by implementing a throttle constructor. The constructor we have in mind will actually make the throttle more flexible by allowing the total number of throttle positions to vary from one throttle to another. We will no longer be restricted to throttles with only six positions. For example, a lawn mower throttle might need only four positions, whereas a 40-position throttle could be used for a rocket that needs finer control.

### adding a constructor to the throttle class

Our throttle constructor has one parameter, which tells the total number of positions that the throttle contains. We do not need a second parameter for the current throttle position because our constructor will always initialize the current position to zero. Here is the prototype for the new constructor, along with its precondition/postcondition contract:

```
throttle(int size);
// Precondition: 0 < size.
// Postcondition: The throttle has size positions above the shutoff position,
//     and its current position is off.
```

It does look strange, seeing the word throttle used in this way, but we have no choice: The name of the constructor must be the same as the name of the class.

Also notice that the word void does not appear at the front of the prototype, nor is there any other return type for the function. The constructor's prototype is placed in the throttle class definition along with the other member functions' prototypes, as indicated here:

```cpp
class throttle
{
public:
  // CONSTRUCTOR
  throttle(int size);
  // MODIFICATION MEMBER FUNCTIONS
  void shut_off( );
  ...
}
```

This is the prototype for the throttle constructor.

Prototypes for other member functions appear as usual.

We'll look at the implementation of the constructor in a moment, but first let's see some examples of using the constructor in declarations of throttle objects. For example, here are the declarations of two throttles:

```cpp
throttle mower_control(4);
throttle apollo(40);
```

After these declarations, each throttle is shut off. The mower_control has four positions, and the apollo has 40.

Often it is useful to provide several different constructors, each of which does a different kind of initialization. For instance, suppose many of our throttles require just one on position—a kind of all-or-nothing throttle. Then we could provide a second constructor with no parameters. The second constructor gives the throttle just one on position, and sets the current position to zero. The prototype for this constructor is shown here:

```cpp
throttle( );
// Precondition: None.
// Postcondition: The throttle has one position above the shutoff position,
//     and its current position is off.
```

A constructor with no parameters is called a default constructor. Here is a declaration of two throttles, with the first using the default constructor and the second using the other constructor:

```cpp
throttle toggle;
throttle complicated(100);
```

When toggle uses the default constructor, there is no argument list—not even a pair of parentheses. In other words, to use the default constructor, just declare an object with no argument list. The default constructor will be called.

You may declare as many constructors as you like—one for each different way of initializing an object. Each constructor must have a distinct parameter list so that the compiler can tell them apart. Only one default constructor is allowed.

To implement our new constructors, we need a new private member variable called top_position, which keeps track of the maximum position of the throttle. The default constructor sets top_position to 1, and the other constructor sets top_position according to the constructor's size parameter. The complete new class definition, along with the implementations of the new constructors, is given in Figure 2.3.

## FIGURE 2.3 Constructors for the Throttle

### A Class Definition

```cpp
class throttle
{
public:
// CONSTRUCTORS
throttle( );
throttle(int size);
// MODIFICATION MEMBER FUNCTIONS
void shut_off( );
void shift(int amount);
// CONSTANT MEMBER FUNCTIONS
double flow( ) const;
bool is_on( ) const;
private:
int top_position;
int position;
};
```

prototype for the default constructor

prototype for the other constructor

A new private member variable keeps track of how many positions the throttle has.

### Implementations of the Constructors

```cpp
throttle::throttle( )
{
top_position = 1;
position = 0;
}

throttle::throttle(int size)
// Library facilities used: cassert
{
assert(0 < size);
top_position = size;
position = 0;
}
```

## What Happens If You Write a Class with No Constructors?

If you write a class with no constructors, then the compiler automatically creates a simple default constructor. This automatic default constructor doesn't do much work. It just calls the default constructor for the member variables that are objects of some other class. Generally, you should write your own constructors, including your own default constructor, rather than depending on the automatic default constructor.

## ALWAYS PROVIDE CONSTRUCTORS

When you write a class, and you define the constructors, each variable of the class will have one of your constructors called when the variable is declared. This increases the reliability of programs by reducing the chance of using uninitialized variables. We also recommend that you define a default constructor for each of your classes. This also allows programmers to declare a variable of your class, without having to provide any arguments for a constructor.

## Revising the Throttle's Member Functions

Because we added a new member variable, top_position, we must revise the member functions to use top_position rather than the number 6 for the number of positions. For example, here is the revised implementation of shift:

```cpp
void throttle::shift(int amount)
// Postcondition: The throttle's position has been moved by amount (but
// not below 0 or above the top position.
{
    position += amount;
    if (position < 0)
        position = 0;
    else if (position > top_position)
        position = top_position;
}
```

Notice that we no longer need a precondition, because we are guaranteed to have one of the constructors called. When there is no precondition you may omit it, as we have done here, or you may list the precondition as "None."

## Inline Member Functions

We'll use a new technique to revise the other three member functions. The technique is to place the complete definitions of shut_off, flow, and is_on inside the class definition, as shown in the three highlighted lines of Figure 2.4.

The use of double in the definition of flow changes top_position from an integer to a double number (otherwise the division will perform an integer
