
There are a few disadvantages to vectors when compared to arrays, including:

- Vectors require a bit of extra memory as overhead.
- There can be a performance cost when a vector grows in size.
- Vectors may not be available on some game console systems.

Overall, vectors (and the STL) can be a welcome tool in most any project.

## Introducing the Hero’s Inventory 2.0 Program

From the user’s point of view, the Hero’s Inventory 2.0 program is similar to its predecessor, the Hero’s Inventory program from Chapter 3. The new version stores and works with a collection of string objects that represent a hero’s inventory. However, from the programmer’s perspective the program is quite different. That’s because the new program uses a vector instead of an array to represent the inventory. Figure 4.1 shows the results of the program.

![](img/c7e8651578bccd573227f684823b8754_139_0.png)

Figure 4.1
This time the hero’s inventory is represented by a vector.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 4 folder; the filename is heros_inventory2.cpp.

```
cout << inventory[i] << endl;
}

cout << "\nYou were robbed of all of your possessions by a thief.";
inventory.clear();
if (inventory.empty())
{
    cout << "\nYou have nothing.\n";
}
else
{
    cout << "\nYou have at least one item.\n";
}

return 0;
}
```

## Preparing to Use Vectors

Before I can declare a vector, I have to include the file that contains its definition:

```
#include <vector>
```

All STL components live in the std namespace, so by using the following code (as I typically do) I can refer to a vector without having to precede it with std::

```
using namespace std;
```

## Declaring a Vector

Okay, the first thing I do in main() is declare a new vector.

```
vector<string> inventory;
```

The preceding line declared an empty vector named inventory, which can contain string object elements. Declaring an empty vector is fine because it grows in size when you add new elements.

To declare a vector of your own, write vector followed by the type of objects you want to use with the vector (surrounded by the < and > symbols), followed by the vector name.

## Hint

There are additional ways to declare a vector. You can declare one with a starting size by specifying a number in parentheses after the vector name.

```
vector<string> inventory(10);
```

The preceding code declared a vector to hold string object elements with a starting size of 10. You can also initialize all of a vector's elements to the same value when you declare it. You simply supply the number of elements followed by the starting value, as in:

```
vector<string> inventory(10, "nothing");
```

The preceding code declared a vector with a size of 10 and initialized all 10 elements to "nothing". Finally, you can declare a vector and initialize it with the contents of another vector.

```
vector<string> inventory(myStuff);
```

The preceding code created a new vector with the same contents as the vector myStuff.

## Using the push_back() Member Function

Next I give the hero the same three starting items as in the previous version of the program.

```
inventory.push_back("sword");
inventory.push_back("armor");
inventory.push_back("shield");
```

The push_back() member function adds a new element to the end of a vector. In the preceding lines I added "sword", "armor", and "shield" to inventory. As a result, inventory[0] is equal to "sword", inventory[1] is equal to "armor", and inventory[2] is equal to "shield".

## Using the size() Member Function

Next I display the number of items the hero has in his possession.

```
cout << "You have " << inventory.size() << " items.\n";
```

I get the size of inventory by calling the size() member function with inventory.size(). The size() member function simply returns the size of a vector. In this case, it returns 3.

Just as with arrays, you can access the member functions of a vector element by writing the element, followed by the member selection operator, followed by the member function name. Because inventory[0] is equal to "battle axe", inventory[0].size() returns 10.

## Using the pop_back() Member Function

I remove the hero's shield using

```
inventory.pop_back();
```

The pop_back() member function removes the last element of a vector and reduces the vector size by one. In this case, inventory.pop_back() removes "shield" from inventory because that was the last element in the vector. Also, the size of inventory is reduced from 3 to 2.

## Using the clear() Member Function

Next I simulate the act of a thief robbing the hero of all of his items.

```
inventory.clear();
```

The clear() member function removes all of the items of a vector and sets its size to 0. After the previous line of code executes, inventory is an empty vector.

## Using the empty() Member Function

Finally, I check to see whether the hero has any items in his inventory.

```
if (inventory.empty())
{
    cout << "\nYou have nothing.\n";
}
else
{
    cout << "\nYou have at least one item.\n";
}
```

The vector member function empty() works just like the string member function empty(). It returns true if the vector object is empty; otherwise, it returns false. Because inventory is empty in this case, the program displays the message, “You have nothing.”

## USING ITERATORS

Iterators are the key to using containers to their fullest potential. With iterators you can, well, iterate through a sequence container. In addition, important parts of the STL require iterators. Many container member functions and STL algorithms take iterators as arguments. So if you want to reap the benefits of these member functions and algorithms, you've got to use iterators.

## Introducing the Hero's Inventory 3.0 Program

The Hero's Inventory 3.0 program acts like its two predecessors, at least at the start. The program shows off a list of items, replaces the first item, and displays the number of letters in the name of an item. But then the program does something new: It inserts an item at the beginning of the group, and then it removes an item from the middle of the group. The program accomplishes all of this by working with iterators. Figure 4.2 shows the program in action.

![](img/c7e8651578bccd573227f684823b8754_145_0.png)

Figure 4.2
The program performs a few vector manipulations that you can accomplish only with iterators.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 4 folder; the filename is heros_inventory3.cpp.

```
// Hero's Inventory 3.0
// Demonstrates iterators

#include <iostream>
#include <string>
#include <vector>

using namespace std;

int main()
{
    vector<string> inventory;
    inventory.push_back("sword");
    inventory.push_back("armor");
    inventory.push_back("shield");

    vector<string>::iterator myIterator;
    vector<string>::const_iterator iter;

    cout << "Your items:\n";
    for (iter = inventory.begin(); iter != inventory.end(); ++iter)
    {
        cout << *iter << endl;
    }

    cout << "\nYou trade your sword for a battle axe.";
    myIterator = inventory.begin();
    *myIterator = "battle axe";
    cout << "\nYour items:\n";
    for (iter = inventory.begin(); iter != inventory.end(); ++iter)
    {
        cout << *iter << endl;
    }

    cout << "\nThe item name " << *myIterator << " has ";
    cout << (*myIterator).size() << " letters in it.\n";

    cout << "\nThe item name " << *myIterator << " has ";
    cout << myIterator->size() << " letters in it.\n";

    cout << "\nYou recover a crossbow from a slain enemy.";
    inventory.insert(inventory.begin(), "crossbow");
    cout << "\nYour items:\n";
    for (iter = inventory.begin(); iter != inventory.end(); ++iter)
    {
        cout << *iter << endl;
    }

    cout << "\nYour armor is destroyed in a fierce battle.";
    inventory.erase((inventory.begin() + 2));
    cout << "\nYour items:\n";
    for (iter = inventory.begin(); iter != inventory.end(); ++iter)
    {
        cout << *iter << endl;
    }

    return 0;
}
```

## Declaring Iterators

After I declare a vector for the hero's inventory and add the same three string objects from the previous incarnations of the program, I declare an iterator.

```
vector<string>::iterator myIterator;
```

The preceding line declares an iterator named myIterator for a vector that contains string objects. To declare an iterator of your own, follow the same pattern. Write the container type, followed by the type of objects the container will hold (surrounded by the < and > symbols), followed by the scope resolution operator (the :: symbol), followed by the type of iterator, followed by a name for your new iterator.

So what are iterators? Iterators are values that identify a particular element in a container. Given an iterator, you can access the value of the element. Given the right kind of iterator, you can change the value. Iterators can also move among elements via familiar arithmetic operators.
