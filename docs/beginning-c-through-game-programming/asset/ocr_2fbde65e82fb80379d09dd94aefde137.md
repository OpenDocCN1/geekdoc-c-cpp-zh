Post-it note on a specific element in inventory. Once I've done that, I can access the element or even change it through the iterator.

Next, I declare another iterator.

```
vector<string>::const_iterator iter;
```

The preceding line of code creates a constant iterator named iter for a vector that contains string objects. A constant iterator is just like a regular iterator except that you can't use it to change the element to which it refers; the element must remain constant. You can think of a constant iterator as providing read-only access. However, the iterator itself can change. This means you can move iter all around the vector inventory as you see fit. You can't, however, change the value of any of the elements through iter. With a constant iterator the Post-it can change, but the thing it's stuck to can't.

Why would you want to use a constant iterator if it's a limited version of a regular iterator? First, it makes your intentions clearer. When you use a constant iterator, it's clear that you won't be changing any element to which it refers. Second, it's safer. You can use a constant iterator to avoid accidentally changing a container element. (If you attempt to change an element through a constant iterator, you'll generate a compile error.)

# Trap

Using push_back() might invalidate all iterators referencing the vector.

Is all of this iterator talk a little too abstract for you? Are you tired of analogies about Post-it notes? Fear not—next, I put an actual iterator to work.

# Looping through a Vector

Next, I loop through the contents of the vector and display the hero's inventory.

```
cout << "Your items:\n";
for (iter = inventory.begin(); iter != inventory.end(); ++iter)
{
    cout << *iter << endl;
}
```

In the preceding code, I use a for loop to move from the first to the last element of inventory. At this general level, this is exactly how I looped through the