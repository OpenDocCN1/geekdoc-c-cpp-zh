The organism class is not hard to implement, and we’ll leave its implementation up to you. But we will give one example of using the class. Movie buffs may recall the 1958 film The Blob. The Blob came to Earth from outer space at a mere 20 ounces, but “untroubled by conscience or intellect,” it absorbs anything and anyone in its path. Without giving away the whole plot, let’s suppose that the Blob grows at the astonishing rate of 100,000 ounces per week for three weeks. Then our hero (Steve McQueen) manages to reverse its growth to a rate of negative 80,000 ounces per week. A program to simulate the movie plot is shown in Figure 14.6. The program assumes that the organism class is implemented with a header file called organism.h.

# The animal Class: A Derived Class with New Private Member Variables

Now we will implement a class that can be used to simulate an animal. Since an animal is-an organism, we will declare the animal class as a derived class of the organism class. In our design, an animal is an organism that must consume a given amount of food each week to survive. If a week has passed and the animal has consumed less than its required amount of food, then death occurs. With this in mind, the animal class will have two new private member variables, which are not part of the organism class, as shown in this partial definition:

```
class animal : public organism
{
public:
    || We discuss the animal's public members in a moment.
private:
    double need_each_week;
    double eaten_this_week;
};
```

The first new member variable, need_each_week, keeps track of how many ounces of food the animal must eat each week in order to survive. The second new member variable, eaten_this_week, keeps track of how many ounces of food the animal has eaten so far this week.

When a derived class has some new member variables, it will usually need a new constructor to initialize those member variables. This is the first example that we have seen where derived class has a new constructor rather than using the automatic constructors that were described on page 687.

# How to Provide a New Constructor for a Derived Class

When a derived class has a new constructor, the prototype for the new constructor appears in the public portion of the class definition, just like any other constructor. In the case of the animal, the new constructor will have three arguments. The first two arguments are the same as the arguments for any organism, providing the initial size and the initial growth rate. The third argument will indicate how much food the animal needs, in ounces per week. Thus, the start of the animal's public section is given next.