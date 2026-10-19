
## General Tips on Pointers

With many types of defects, locating the error is the easiest part of dealing with the error and correcting it is the hard part. Pointer errors are different. A pointer error is usually the result of a pointer’s pointing somewhere it shouldn’t. When you assign a value to a bad pointer variable, you write data into an area of memory you shouldn’t. This is called “memory corruption.” Sometimes memory corruption produces horrible, fiery system crashes; sometimes it alters the results of a calculation in another part of the program; sometimes it causes your program to skip routines unpredictably; and sometimes it doesn’t do anything at all. In the last case, the pointer error is a ticking time bomb, waiting to ruin your program five minutes before you show it to your most important customer. Symptoms of pointer errors tend to be unrelated to causes of pointer errors. Thus, most of the work in correcting a pointer error is locating the cause.

Working with pointers successfully requires a two-pronged strategy. First, avoid installing pointer errors in the first place. Pointer errors are so difficult to find that extra preventive measures are justified. Second, detect pointer errors as soon after they are coded as possible. Symptoms of pointer errors are so erratic that extra measures to make the symptoms more predictable are justified. Here’s how to achieve these key goals:

![](img/649c8eee28c38ca1e062691e45dc9883_361_0.png)

- **Isolate pointer operations in routines or classes** Suppose you use a linked list in several places in a program. Rather than traversing the list manually each place it’s used, write access routines such as `NextLink()`, `PreviousLink()`, `InsertLink()`, and `DeleteLink()`. By minimizing the number of places in which pointers are accessed, you minimize the possibility of making careless mistakes that spread throughout your program and take forever to find. Because the code is then relatively independent of data-implementation details, you also improve the chance that you can reuse it in other programs. Writing routines for pointer allocation is another way to centralize control over your data.

- **Declare and define pointers at the same time** Assigning a variable its initial value close to where it is declared is generally good programming practice, and it’s all the more valuable when working with pointers. Here is an example of what not to do:

![](img/649c8eee28c38ca1e062691e45dc9883_361_1.png)

**C++ Example of Bad Pointer Initialization**

```cpp
Employee *employeePtr;
// lots of code
...
employeePtr = new Employee;
```

- 2. Set the first 4 bytes to a dog-tag value, and then return a pointer to the memory that starts after that.

![](img/649c8eee28c38ca1e062691e45dc9883_363_0.png)

- 3. When the time comes to delete the pointer, check the tag.

![](img/649c8eee28c38ca1e062691e45dc9883_363_1.png)

- 4. If the tag is OK, set it to 0 or some other value that you and your program recognize as an invalid tag value. You don’t want the value to be mistaken for a valid tag after the memory has been freed. Set the data to 0, 0xCC, or some other non-random value for the same reason.

- 5. Finally, delete the pointer.

![](img/649c8eee28c38ca1e062691e45dc9883_363_2.png)

Putting a dog tag at the beginning of the memory block you’ve allocated allows you to check for redundant attempts to deallocate the memory block without needing to maintain a list of all the memory blocks you’ve allocated. Putting the dog tag at the end of the memory block allows you to check for overwriting memory beyond the location that was supposed to be used. You can use tags at the beginning and the end of the block to accomplish both objectives.

You can use this approach in concert with the reasonableness check suggested earlier—checking that the pointers are between StartData and EndData. To be sure that a pointer points to a reasonable location, rather than checking for a probable range of memory, check to see that the pointer is in the list of allocated pointers.

You could check the tag field just once before you delete the variable. A corrupted tag would then tell you that sometime during the life of that variable its contents were corrupted. The more often you check the tag field, however, the closer to the root of the problem you will detect the corruption.

- **Add explicit redundancies** An alternative to using a tag field is to use certain fields twice. If the data in the redundant fields doesn’t match, you know memory has been corrupted. This can result in a lot of overhead if you manipulate pointers directly. If you isolate pointer operations in routines, however, it adds duplicate code in only a few places.

- **Use extra pointer variables for clarity** By all means, don’t skimp on pointer variables. The point is made elsewhere that a variable shouldn’t be used for more than one purpose. This is especially true for pointer variables. It’s hard enough to figure out what someone is doing with a linked list without having to figure out why one genericLink variable is used over and over again or what pointer->next->last->next is pointing at. Consider this code fragment:

**C++ Example of Traditional Node Insertion Code**

```cpp
void InsertLink(
    Node *currentNode,
    Node *insertNode
) {
    // insert "insertNode" after "currentNode"
    insertNode->next = currentNode->next;
    insertNode->previous = currentNode;
    if ( currentNode->next != NULL ) {
        currentNode->next->previous = insertNode;
    }
    currentNode->next = insertNode;
}
```

This line is needlessly difficult.

This is traditional code for inserting a node in a linked list, and it’s needlessly hard to understand. Inserting a new node involves three objects: the current node, the node currently following the current node, and the node to be inserted between them. The code fragment explicitly acknowledges only two objects: insertNode and currentNode. It forces you to figure out and remember that currentNode->next is also involved. If you tried to diagram what is happening without the node originally following currentNode, you would get something like this:

![](img/649c8eee28c38ca1e062691e45dc9883_364_0.png)

A better diagram would identify all three objects. It would look like this:

![](img/649c8eee28c38ca1e062691e45dc9883_364_1.png)

Here’s code that explicitly references all three of the objects involved:

**C++ Example of More Readable Node-Insertion Code**

```cpp
void InsertLink(
    Node *startNode,
    Node *newMiddleNode
) {
    // insert "newMiddleNode" between "startNode" and "followingNode"
    Node *followingNode = startNode->next;
    newMiddleNode->next = followingNode;
    newMiddleNode->previous = startNode;
    if ( followingNode != NULL ) {
        followingNode->previous = newMiddleNode;
    }
    startNode->next = newMiddleNode;
}
```

This code fragment has an extra line of code, but without the first fragment’s `currentNode->next->previous`, it’s easier to follow.

- **Simplify complicated pointer expressions** Complicated pointer expressions are hard to read. If your code contains expressions like p->q->r->s.data, think about the person who has to read the expression. Here’s a particularly egregious example:

**C++ Example of a Pointer Expression That’s Hard to Understand**

```cpp
for ( rateIndex = 0; rateIndex < numRates; rateIndex++ ) {
    netRate[ rateIndex ] = baseRate[ rateIndex ] * rates->discounts->factors->net;
}
```

Complicated expressions like the pointer expression in this example make for code that has to be figured out rather than read. If your code contains a complicated expression, assign it to a well-named variable to clarify the intent of the operation. Here’s an improved version of the example:

**C++ Example of Simplifying a Complicated Pointer Expression**

```cpp
quantityDiscount = rates->discounts->factors->net;
for ( rateIndex = 0; rateIndex < numRates; rateIndex++ ) {
    netRate[ rateIndex ] = baseRate[ rateIndex ] * quantityDiscount;
}
```

With this simplification, not only do you get a gain in readability, but you might also get a boost in performance from simplifying the pointer operation inside the loop. As usual, you’d have to measure the performance benefit before you bet any folding money on it.

- **Draw a picture** Code descriptions of pointers can get confusing. It usually helps to draw a picture. For example, a picture of the linked-list insertion problem might look like the one shown in Figure 13-2.

**Cross-Reference** Diagrams such as the one in Figure 13-2 can become part of the external documentation of your program. For details on good documentation practices, see Chapter 32, “Self-Documenting Code.”

![](img/649c8eee28c38ca1e062691e45dc9883_365_0.png)

**Figure 13-2** An example of a picture that helps us think through the steps involved in relinking pointers.
