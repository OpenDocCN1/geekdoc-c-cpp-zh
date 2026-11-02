In summary, when you analyze a problem description, you will want to carry out these tasks:

+   - Find the concepts that you need to implement as classes. Often, these will be nouns in the problem description.
+   - Find the responsibilities of the classes. Often, these will be verbs in the problem description.
+   - Find relationships between the classes that you have discovered. In this section, we described the aggregation relationship. In the next chapter, you will learn about another important relationship between classes, called inheritance.

![](bbox=[0.15, 0.33, 0.2, 0.4])

# Programming Tip 9.3

# Make Parallel Vectors into Vectors of Objects

Sometimes, you find yourself using vectors of the same length, each of which stores a part of what conceptually should be an object. In that situation, it is a good idea to reorganize your program and use a single vector whose elements are objects.

For example, suppose an invoice contains a series of item descriptions and prices. One solution is to keep two vectors:

```
vector<string> descriptions;
vector<double> prices;
```

Each of the vectors will have the same length, and the ith slice, consisting of descriptions[i] and prices[i], contains data that needs to be processed together. These vectors are called parallel vectors (see Figure 7).

![](bbox=[0.4, 0.7, 0.85, 0.78])

Figure 7 Parallel Vectors

Parallel vectors become a headache in larger programs. The programmer must ensure that the vectors always have the same length and that each slice is filled with values that actually belong together. Moreover, any function that operates on a slice must get all of the vectors as arguments, which is tedious to program.

> Avoid parallel vectors by changing them into vectors of objects.

The remedy is simple. Look at the slice and find the concept that it represents. Then make the concept into a class. In this example, each slice contains the description and price of an item; turn this into a class.

```
class Item
{
public:
private:
    string description;
    double price;
};
```