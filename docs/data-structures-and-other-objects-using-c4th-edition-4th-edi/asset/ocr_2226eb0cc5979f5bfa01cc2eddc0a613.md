Here is the implementation of our animal constructor, with the member initialization list highlighted:

```
```cpp
animal::animal
(double init_size, double init_rate, double init_need)
: organism(init_size, init_rate), // Activate base class constructor
  need_each_week(init_need), // Initial value for need_each_week
  eaten_this_week(0) // Initial value for eaten_this_week is 0
{
} // Because of the initialization list, this constructor has no work.
```
```

By the way, in the animal class definition, we will provide each of the parameters with a default argument, so that this constructor can be used as a default constructor for the animal.

# The Other Animal Member Functions

The animal has four new member functions that deal with eating, and the simulate_week member function must also be overridden. The four new functions are called assign_need, eat, still_need, and total_need. We'll discuss each of these member functions now.

**The assign_need function.** This member function has this prototype:

```
```cpp
void assign_need(double new_need);
```
```

The member function is activated when a simulation needs to specify how much food an animal must eat to survive a week. For example, if spot is an animal that needs 30 ounces of food to survive a week, then spot.assign_need(30) is activated. During a simulation, the food requirements may change, so that assign_need can be activated several times with different arguments.

**The eat function.** Whenever the animal, spot, eats m ounces of food, the member function spot.eat(m) records this event. Here's the prototype of the member function:

```
```cpp
void eat(double amount);
```
```

The amount of food that has been eaten during the current week is stored in a private member variable, eaten_this_week. So, activating eat(m) will simply add m to eaten_this_week.

**Overriding the simulate_week function.** The animal must do some extra work in its simulate_week member function. Therefore, it will override the organism's simulate_week function. The animal's simulate_week will first activate organism::simulate_week to carry out whatever work an ordinary