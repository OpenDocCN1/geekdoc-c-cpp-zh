
For example, our cuckoo clock has an automatic default constructor that is activated in an object declaration such as this:

```
cuckoo_clock noisy;
```

The cuckoo_clock's automatic default constructor will activate the ordinary clock default constructor for noisy, initializing any private member variables of the ordinary clock. Remember, these private member variables are present in any cuckoo clock, and therefore they must be initialized even though there is no way to directly access these member variables.

### The automatic copy constructor.

If a derived class does not define a copy constructor of its own, then C++ will automatically provide a copy constructor. This copy constructor is similar to the automatic default constructor in that it carries out two steps: (1) Activate the copy constructor for the base class (to copy any member variables that the base class uses), then (2) activate copy constructors for any new member variables that the derived class has but the base class does not have. The copy constructors that are activated in Steps 1 and 2 may themselves be automatic copy constructors, or they may be specially written to accomplish correct copying of dynamic data structures.

## Using a Derived Class

We now know enough to write a bit of sample code that uses a derived class:

```
cuckoo_clock noisy;
int minutes;
cout << "How many minutes should I advance the clock? ";
cin >> minutes;
noisy.advance(minutes);
if (noisy.is_cuckooing())
    cout << "Cuckoo cuckoo cuckoo." << endl;
else
    cout << "All's quiet on the cuckoo front." << endl;
```

The key feature is that a cuckoo clock may use ordinary clock member functions (such as advance), and it may also use the new is_cuckooing function. The inheritance is accomplished with little work on our part. We need to write only the body of is_cuckooing; none of the ordinary clock functions need to be rewritten for the cuckoo clock.

There's another advantage to derived classes: An object of the derived class may be used at any location where the base class is expected. For example, suppose we overload the "less than" operator to compare the times on two clocks, as shown in Figure 14.3 on page 689. We can use this relational operator to compare two ordinary clocks, but we can also compare any of the clock's derived classes. Here is some sample code:

```
cuckoo_clock sunrise, your_time;
int minutes;

sunrise.advance(60 * 6); // Set the sunrise for 6 A.M.
cout << "How many minutes do I advance your clock?" << endl;
cin >> minutes;
your_time.advance(minutes);

if (sunrise < your_time)
    cout << "That's before sunrise!" << endl;
else
    cout << "That's not before sunrise." << endl;
```

## FIGURE 14.3 Implementation of the Less-Than Operator for Clocks

## A Function Implementation

```
bool operator < (const clock& c1, const clock& c2)
// Postcondition: Returns true if the time on c1 is earlier than the time on c2
//     over a usual day (starting at midnight); otherwise returns false.
{
    // Check whether one is morning and the other is not.
    if (c1.is_morning() && !c2.is_morning())
        return true;
    else if (c2.is_morning() && !c1.is_morning())
        return false;

    // Check whether one is 12 o'clock and the other is not.
    else if ((c1.get_hour() == 12) && (c2.get_hour() != 12))
        return true;
    else if ((c2.get_hour() == 12) && (c1.get_hour() != 12))
        return false;

    // Check whether the hours are different from each other.
    else if (c1.get_hour() < c2.get_hour())
        return true;
    else if (c2.get_hour() < c1.get_hour())
        return false;

    // The hours are the same, so check the minutes.
    else if (c1.get_minute() < c2.get_minute())
        return true;
    else
        return false;
}
```

In fact, we can even use the “less than” operator to compare an ordinary clock with a cuckoo_clock, or to compare two objects from different derived classes. Any functions that you write to manipulate a clock will also be able to manipulate all of the clock’s derived classes. Without derived classes, we would need to write a separate function for each kind of clock that we want to manipulate.

## The Automatic Assignment Operator for a Derived Class

If a derived class does not define its own assignment operator, then C++ will automatically provide an assignment operator. This automatic assignment operator is similar to the automatic constructors, carrying out two steps: (1) Activate the assignment operator for the base class (to copy any member variables that the base class uses), then (2) activate the assignment operator for any new member variables that the derived class has but the base class does not have. The assignment operators that are activated in Steps 1 and 2 may themselves be automatic assignment operators, or they may be specially written to accomplish correct copying of dynamic data structures.

Assignments are also allowed from a derived class to the base class, for example:

```
clock ordinary;
cuckoo_clock fancy;
fancy.advance(60);
ordinary = fancy;
```

Advance the fancy clock to 1 A.M. and assign the ordinary clock to equal the fancy clock.

The assignment ordinary = fancy is permitted because a cuckoo clock (such as fancy) can be used at any point where an ordinary clock is expected. Therefore, the assignment will activate the assignment operator for an ordinary clock (using fancy as if it were just an ordinary clock).

On the other hand, an assignment in the other direction, fancy = ordinary, is forbidden because an object of the base class (the ordinary clock) cannot be used as if it were an object of the derived class (the cuckoo clock).

- Allowed:
  When a base class is public, an object of a derived class may be used as if it were an object of the base class.

- Forbidden:
  But an object of the base class cannot usually be used as if it were an object of the derived class.

## The Automatic Destructor of a Derived Class

Derived classes have one last automatic feature. If a class does not have a declared destructor, then C++ provides an automatic destructor that carries out two steps: (1) The destructors are called for any member variables that the derived class has, but the base class does not have, then (2) the destructor is called for the base class. Notice that an automatic destructor works differently than an automatic constructor: An automatic destructor first activates the destructors for member variables and then activates the destructor for the base class. But an automatic constructor first activates the constructor for the base class, and then activates the constructors for member variables.

## Overriding Inherited Member Functions

A derived class must sometimes perform actions differently from the way the base class does. For example, the original clock provides the current hour via get_hour, using a 12-hour clock. Suppose we want to implement a derived class that provides its hour on a 24-hour basis, ranging from 0 to 23. The new clock can be defined as a derived class called clock24. The clock24 class inherits everything from the original clock, but it provides a new get_hour member function. This is called overriding an inherited member function.

To override an inherited member function, the derived class uses a new prototype for the overridden function, as shown here:

```
class clock24 : public clock
{
public:
    int get_hour() const; // Overridden from the clock class
};
```

Now we are free to define a new implementation of clock24::get_hour. Within this implementation, we can use any of the ordinary clock functions, and we can even use the get_hour member function from the ordinary clock. The notation for using the ordinary clock's get_hour function is to place the scope resolution operator, clock::, in front of the function call. So, when we write clock::get_hour(), we are activating the original clock's get_hour function. Here's the complete implementation of clock24::get_hour:

use the scope resolution operator to call the original version of the function

```
int clock24::get_hour() const
{
    int ordinary_hour;

    ordinary_hour = clock::get_hour();
    if (is_morning())
    {
        if (ordinary_hour == 12)
            return 0;
        else
            return ordinary_hour;
    }
    else
    {
        if (ordinary_hour == 12)
            return 12;
        else
            return ordinary_hour + 12;
    }
}
```
