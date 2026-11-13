# Details of the Story-Writing Program

The story-writing program uses a function, get_items, which is actually a template function with this specification:

```
template <class Item, class SizeType, class MessageType>
void get_items(bag<Item>& collection, SizeType n, MessageType description);
// Postcondition: The description has been written as a prompt to the
// screen. Then n items have been read from cin and added to the collection.
```

The function uses the third parameter, description, as part of a prompt that asks the user to type n items. For example, if description is the string constant "first names" and n is 4, then the get_items function writes this prompt:

> Please type 4 first names, separated by spaces.
> Press the <return> key after the final entry:

The function then reads n items and places them in the bag with the insert member function. Because the function is a template function that depends on the Item data type, we can use the function with any kind of bag—with a bag of strings, or a bag of integers, or even some other kind of bag. In fact, the template prefix indicates that the function depends on three classes:

+   * class Item: This is the type of the item in the bag.
+   * class SizeType: This is the type of the second parameter, n. It may be any integer data type such as int or size_t.
+   * class MessageType: This may be any printable data type such as a string constant or even a string variable.

The literary merit of the program's story is debatable, but the ability to use several different kinds of bags in the same program is clearly important.

# Self-Test Exercises for Section 6.2

+   9. When you implement a template class, the entire implementation file is included in the header file. Why is this needed?
+   10. When you write a template class, where does the template prefix occur?
+   11. Why should you use directive to be avoided in an implementation file of a template class?
+   12. When does instantiation of a template parameter occur?
+   13. Name two places in the bag template class where the name bag is not changed to bag<Item>.
+   14. Describe the purpose of the C++ keyword typename as used in this section.