# Solutions to Chapter 12 | System Design and Memory Limits

12.2 How would you design the data structures for a very large social network (Facebook, LinkedIn, etc)? Describe how you would design an algorithm to find the connection, or between two people (e.g., Me -> Bob -> Susan -> Jason -> You).

# SOLUTION

Approach:
Forget that we're dealing with millions of users at first. Design this for the simple case.

We can construct a graph by assuming every person is a node and if there is an edge between two nodes, then the two people are friends with each other.

```
class Person {
    Person[] friends;
    // Other info
}
```

If I want to find the connection between two people, I would start with one person and do a simple breadth first search.

But... oh no! Millions of users!

When we deal with a service the size of Orkut or Facebook, we cannot possibly keep all of our data on one machine. That means our simpel Person data structure from above doesn't work—our friends may not live on the same machine as us. Instead, we can replace our list of friends with a list of their IDs, and traverse as follows:

+   1. For each friend ID: int machine_index = lookupMachineForUserId(id);
2. Go to machine_index
3. Person friend = lookupFriend(machine_index);

There are more optimizations and follow up questions here than we could possibly discuss, but here are a few thoughts.

Optimization: Reduce Jumps

Jumping from one machine to another is expensive. Instead of randomly jumping from machine to machine with each friend, try to batch these jumps—e.g., if 5 of my friends live on one machine, I should look them all up at once.

Optimization: Smart Division of People and Machines

People are much more likely to be friends with people who live in the same country as them. Rather randomly dividing people up across machines, try to divvy them up by country, city, state, etc. This will reduce the number of jumps.

Question: Breadth First Search usually requires "marking" a node as visited. How do you do that in