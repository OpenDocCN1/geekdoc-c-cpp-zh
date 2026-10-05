
# Log N

An algorithm with O(log N) performance typically divides the number of items it must consider by a fixed fraction at every step.

## LOGARITHMS
The logarithm of a number in a certain log base is the power to which the base must be raised to get a certain result. For example, log2[8] is 3 because 2^3 = 8. Here, 2 is the log base.

Often in the algorithms base is 2 because the inputs are being divided into two groups repeatedly. As you'll see shortly, the log base isn't really important in Big O notation, it is usually omitted.

For example, Figure 1-1 shows a sorted complete binary tree. It's a binary tree because every node has at most two branches. It's a complete tree because every level (except possibly the last) is completely full and all the nodes in the last level are grouped on the left side. It's a sorted tree because every node's value lies between the values of its left and right child nodes.

![](img/fefa42765c0b410af6705110aea7c0cb_35_0.png)

**Figure 1-1:** Searching a full binary tree takes O(log N) steps.

The following pseudocode shows one way you might search the tree shown in Figure 1-1 to find a particular item.

```
Node: FindItem(Integer: target_value)
Node: test_node = <root of tree>

Do Forever
// If we fell off the tree. The value isn't present.
If (test_node == null) Return null

If (target_value == test_node.Value) Then
    // test_node holds the target value. This is the node we want
    Return test_node
Else If (target_value < test_node.Value) Then
    // Move to the left child.
    test_node = test_node.LeftChild
Else
    // Move to the right child.
    test_node = test_node.RightChild
End
End Do
End FindItem
```

Chapter 10 covers trees in detail, but yet you should be able to get the gist of the algorithm from the following discussion.

The algorithm declares and initializes the variable test_node so that it points to the root at the top of the tree. (Traditionally, trees in computer programs are drawn with the root at the top, unlike real trees.) It enters an infinite loop.

If test_node is null, the target value isn't in the tree, so the algorithm returns null.

> null is a special value that you can assign to a variable that would normally point to an object such as a node in a tree. The null means "This variable doesn't point to anything."

If test_node holds the target value, test_node is the node we're seeking, for is less than the value in test_node, the algorithm sets test_node equal to its left child. (If test_node is at the bottom of the tree, its LeftChild is null, and the algorithm handles the situation next it goes through the loop)

If test_node's value does not equal target_value and is not less than target_value, it must be greater than target_value. In that case, the algorithm sets test_node equal to its right child. (Again, if test_node is at the bottom of the tree, its RightChild is null, and the algorithm handles the next time it goes through the loop).

The variable test_node moves down the tree and eventually either finds the target value or falls off the tree when test_node is null.

Understanding this algorithm's performance becomes a question of how far down the tree test_node must move before it finds target_value or falls off the tree.

Sometimes the algorithm gets lucky and finds the target value right off away. If the target value is 7 in Figure 1-1, the algorithm finds it in one step and stops.

Even if the target value is not at the root—for example, if it's 4—the program might have to check only a bit of a tree before stopping.

In the worst case, however, the algorithm needs to search the tree from top to bottom.

In roughly half the tree's nodes are at the bottom that have missing children. If the tree were a complete tree, with every node having exactly zero or two children, the bottom level would easily hold half the tree's nodes. In if you search for randomly chosen values in the tree, the algorithm will have to travel through most of the tree's height most of the time.

Now the question is, "How tall is the tree?" A full binary tree of height H has 2H nodes. To look at it from the other direction, a full binary tree that contains N nodes has log(N). Because the algorithm searches from top to bottom in the worst (and average) case, and because the tree has a height of roughly log(N), the algorithm runs in O(log2(N)) time.

At this point a curious feature of logarithms comes into play. You can convert a logarithm from base A to base B using this formula:

```
logA(x) = log(x) / logA(B)
```

Setting B = 2, you can use this formula to convert the O(logA(N)) into any other log base A.

```
O(logA(N)) = O(logA(N) / logA(2))
```

The value 1 / log(2) is a constant for any given A, and Big O notation ignores constants, so O(log N) is common for any base.

## Chapter 1 ■ Algorithm Basics

## N
The FindLargest algorithm described in the earlier section “1” has O(N) performance. See that section for an explanation of why it has O(N) performance.

The function N grows more quickly than log(N) and sqrt(N) but still not too quickly, so algorithms that have O(N) performance work quite well.

## N log N
Suppose an algorithm loops over all the items in its problem and then, for each loop, performs some O(log N) calculation on that item. In that case, the algorithm has O(N log N) or O(N log N) performance.

Alternatively, an algorithm might perform some sort of O(log N) operation and, for each step it to do something to the items.

For example, you have built a sorted tree containing N items as described earlier. You also have an array of N values and you want to know which values in the array are also in the tree.

One approach would be to loop through the values in the array. For each value, you could use the method described earlier to search the tree for that value. The algorithm examines N items and for each it performs log(N) steps the total runtime is O(N log).

Many sorting algorithms that work by comparing items have an O(N log N) runtime. In fact, it can be proven that any algorithm that sorts by comparing items must use at least O(N log N) steps, to this is the best you can do, at least in Big O notation. Some algorithms are faster than others because of the constants Big O notation ignores.

## N
An algorithm that loops over all its inputs and then for each input loops over the inputs having O(N²) performance. For example, the ContainsDuplicates algorithm described earlier, in the section “4” runs in O(N²) time. See that section for a description and analysis of the algorithm.

Other powers of N, such as O(N³) and O(N⁴), are possible and obviously slower than O(N²).

## Sqrt N
Some algorithms have O(sqrt(N)) performance (where sqrt is the square root), but they're not common, and now covered in this book.

The function sqrt(N) grows more slowly than log(N).

## Polynomial
An algorithm is said to have polynomial runtime if it involves any polynomial involving N. O(N), O(N²), O(N³) and even O(N⁴) are all polynomial runtimes.

Polynomial runtimes are important in some sense these problems can be solved. The exponential and fractal runtimes described next grow extremely quickly, so algorithms that have those runtimes are practical for very small numbers of inputs.
