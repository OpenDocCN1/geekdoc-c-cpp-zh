
# LISTING 10.12

```
//***************************************************************************
// Searching.java      Author: Lewis/Loftus
//
// Demonstrates the linear search and binary search algorithms.
//***************************************************************************

public class Searching
{
    //---------------------------------------------------------------
    // Searches the specified array of objects for the target using
    // a linear search. Returns a reference to the target object from
    // the array if found, and null otherwise.
    //---------------------------------------------------------------
    public static Comparable linearSearch (Comparable[] list,
                                            Comparable target)
    {
        int index = 0;
        boolean found = false;

        while (!found && index < list.length)
        {
            if (list[index].compareTo(target) == 0)
                found = true;
            else
                index++;
        }

        if (found)
            return list[index];
        else
            return null;
    }

    //---------------------------------------------------------------
    // Searches the specified array of objects for the target using
    // a binary search. Assumes the array is already sorted in
    // ascending order when it is passed in. Returns a reference to
    // the target object from the array if found, and null otherwise.
    //---------------------------------------------------------------
    public static Comparable binarySearch (Comparable[] list,
                                            Comparable target)
    {
        int min=0, max=list.length-1, mid=0;
        boolean found = false;

while (!found && min <= max)
{
    mid = (min+max) / 2;
    if (list[mid].compareTo(target) == 0)
        found = true;
    else
        if (target.compareTo(list[mid]) < 0)
            max = mid-1;
        else
            min = mid+1;
}

if (found)
    return list[mid];
else
    return null;
}
```

Consider the following sorted array of integers:

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 |
|---|---|---|---|---|---|---|---|---|---|----|----|----|----|----|
| 10 | 12 | 18 | 22 | 31 | 34 | 40 | 46 | 59 | 67 | 69 | 72 | 82 | 84 | 98 |

Suppose we were trying to determine if the number 67 is in this list. Initially, the target might be anywhere in the list, or not at all. That is, at first, all items in the search pool are viable candidates.

Instead of starting the search at one end or the other, a binary search begins in the middle of the sorted list. If the target element is not found at that middle element, then the search continues. The middle element of this list is 46, which is not our target, so we must search on. However, since the list is sorted, we know that if 67 is in the list, it will be in the later half of the array. All values at lower indexes are less than 46. Thus, with one comparison, we’ve taken half of the data out of consideration, and we are left with the following viable candidates:

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_544_0.png)

To search the remaining candidates, we once again examine the “middle” element. The middle element is 72, and thus we have still not found the target. But once again, we can eliminate half of the viable candidates (those greater than 72) and we are left with:

Viable Candidates
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14
10 12 18 22 31 34 40 46 59 67 69 72 82 84 98

Employing the same approach again, we select the middle element, 67, and find the element we are seeking. If it had not been our target, we would have continued with this process until we either found the value or eliminated all possible data.

With each comparison, a binary search eliminates approximately half of the remaining data to be searched (it also eliminates the middle element as well). That is, a binary search eliminates half of the data with the first comparison, another quarter of the data with the second comparison, another eighth of the data with the third comparison, and so on. The binary search approach is pictured in Figure 10.5.

The binarySearch method from the Searching class performs a binary search by looping until the target element is found or until the viable candidates drop to zero. Two integer indexes, min and max, are used to define the portion of the array that is still considered viable. When min becomes greater than max, then the viable candidates have been exhausted.

On each iteration of the loop, the midpoint is calculated by dividing the sum of min and max by two. If there are currently an even number of viable candidates, and thus two “middle” values, this calculation discards the fractional remainder and picks the first of the two.

If the target element is not found, the value of min or max is modified to eliminate the appropriate half of the viable candidates. Then the search continues.

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_545_0.png)

FIGURE 10.5 A binary search

Polymorphism provides a means to create elegant versatility in our software. It allows us to apply a consistent approach to inconsistent but related behaviors. We should try to find opportunities in our software systems that lend themselves to polymorphic solutions. We should seek them out, actively and deliberately, before we begin to write code.

Whenever you find situations in which different types of objects perform the same type of behavior, there is an opportunity for a polymorphic solution. The more experience you get, the easier it will be to detect such situations. See if you recognize the opportunity for polymorphism in the following situations:

- Different types of vehicles move in different ways.
- All business transactions for a company must be logged.
- All products produced by a company must meet certain quality standards.
- A hotel needs to plan their remodeling efforts for every room.
- A casino wants to analyze the profit margin for their games.
- A dispatcher must schedule moving vans and personnel based on the job size.
- A drawing program allows the user to draw various shapes.

The common theme in these examples is that the same basic behavior applies to multiple objects, and those behaviors are accomplished differently depending on the specific type of object. Every circle is drawn using the same basic techniques and information, which is different from the information needed and the steps taken to draw a rectangle. Yet both types of shapes get drawn. Different, but similar. Polymorphic.

The example of a drawing program is explored in more detail in the PaintBox case study presented in Appendix J. It follows the refinement of a large program through various stages of its development. The heart of its design is a polymorphic approach to handling the various types of shapes that the user can draw.

Once a polymorphic situation is identified, the specifics of the design can be addressed. In particular, should you use inheritance or interfaces as the mechanism to define polymorphic references? The answer to that question lies in the relationships among the different types of objects involved. If those objects can be related naturally by inheritance, with true is-a relationships, then polymorphism via inheritance is probably the way to go. But if the main thing the objects have in common is their need to be processed in a particular way, then perhaps using an interface to create the polymorphic references is the better solution.

> KEY CONCEPT
> Polymorphism allows us to apply a consistent approach to inconsistent behaviors.

> KEY CONCEPT
> We should hone our design senses to identify situations that lend themselves to polymorphic solutions.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 10.20 Suppose you are designing classes for a banking-related system. Both checking accounts and savings accounts require deposit and withdraw operations. You decide to provide these behaviors using polymorphism. Which polymorphic mechanism (inheritance or interfaces) is best suited for this situation? Provide support for your choice.

SR 10.21 Suppose you are designing classes to help create aquarium-based screen savers. At times, you will want some aquarium objects to “float” from wherever they are to the top of the tank. You decide to provide this behavior using polymorphism. Which polymorphic mechanism (inheritance or interfaces) is best suited for this situation? Provide support for your choice.

SR 10.22 Suppose you are designing classes to support the modeling of rain forest environments. Animal objects, such as butterflies and monkeys, need to grow older periodically. You decide to provide this behavior using polymorphism. Which polymorphic mechanism (inheritance or interfaces) is best suited for this situation? Provide support for your choice.

## 10.7 Event Processing

Let’s revisit the concept of event processing in a Java GUI and see how it relates to polymorphism. As we’ve seen many times in previous examples, in order to respond to an event, we must establish a relationship between an event listener object and a particular component that may fire the event. We establish the relationship between the listener and the component it listens to by making a method call that adds the listener to the component.

For example, suppose a class called MyButtonListener represents an action listener. To set up a listener to respond to a JButton object, we might do the following:

```
JButton button = new JButton();
button.addActionListener (new MyButtonListener());
```

Once this relationship is established, the listener will respond whenever the button fires an action event (because the user pressed it). Now think about the addActionListener method carefully. It is a method of the JButton class, which was written by someone at Sun Microsystems years ago. On the other hand, we might have written the MyButtonListener class today. So how can a method written years ago take a parameter whose class was just written?
