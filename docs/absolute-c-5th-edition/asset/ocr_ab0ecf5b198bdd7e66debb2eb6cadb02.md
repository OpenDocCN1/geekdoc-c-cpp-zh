# Programming with Inheritance

# 639

# EXAMPLE: (continued)

The member function backup copies data from the partially filled array (a and used) to the backup copies b and usedB with the following code:

```
usedB = used;
for (int i = 0; i < usedB; i++)
nb[i] = a[i];
```

You should note the member variables a and used in the base class are protected and not private. The preceding code would be illegal because it accesses the inherited member variables a and used by name.

The member function restore simply reverses things and copies from b and used to a.

The definition of the overloaded assignment operator for the derived class PFArrayDBak begins with an invocation of the assignment operator for the base class PFArrayD. This copies all data from the member variables a, used, and capacity from the object on the right-hand side of the assignment operator (from the parameter rightSide) to the object on the left-hand side of the assignment operator (the calling object). We are relying on the fact that this was done properly in the definition of the overloaded assignment operator in the base class. That is, we rely behave correctly when the same object (for the inherited part) occurs on both sides of the assignment operator, and we assume the copying actions make an independent copy of the array a. In the code of the overloaded assignment operator for the derived class PFArrayDBak needs to create a similarly independent copy of the array b.

Since the objects on the right and left sides of the assignment operators may have different capacities, we must create a new array b (in most cases). This is as follows:

```
if (oldCapacity != rightSide.capacity)
{
  delete [] b;
  b = new double[rightSide.capacity];
}
```

Note that the Boolean expression in the if statement ensures that b will not be deleted when the objects on either side of the assignment operator have the same capacity. In particular, this ensures that when the same object appears on both sides of the assignment operator, the array b is not deleted. After this, the copying of data is routine.

Note that the destructor for the class PFArrayDBak has no explicit mention of the inherited member variable a. It simply sends the b array back to the frestore for recycling with the following statement.

(continued)