
This results in an efficient and safe function call. It’s efficient because only a reference is passed; the vector is not copied. It’s safe because the reference to the vector is a constant reference; inventory can’t be changed by display().

## Trap

You can’t modify a parameter marked as a constant reference. If you try, you’ll generate a compile error.

Next, display() lists the elements in the vector using a constant reference to inventory. Then control returns to main() and the program ends.

## DECIDING HOW TO PASS ARGUMENTS

At this point you’ve seen three different ways to pass arguments—by value, as a reference, and as a constant reference. So how do you decide which method to use? Here are some guidelines:

- **By value.** Pass by value when an argument variable is one of the fundamental built-in types, such as bool, int, or float. Objects of these types are so small that passing by reference doesn’t result in any gain in efficiency. You should also pass by value when you want the computer to make a copy of a variable. You might want to use a copy if you plan to alter a parameter in a function, but you don’t want the actual argument variable to be affected.

- **As a constant reference.** Pass a constant reference when you want to efficiently pass a value that you don’t need to change.

- **As a reference.** Pass a reference only when you want to alter the value of the argument variable. However, you should try to avoid changing argument variables whenever possible.

## RETURNING REFERENCES

Just like when you pass a value, when you return a value from a function, you’re really returning a copy of the value. Again, for values of the basic built-in types, this isn’t a big deal. However, it can be an expensive operation if you’re returning a large object. Returning a reference is an efficient alternative.

## Introducing the Inventory Referencer Program

The Inventory Referencer program demonstrates returning references. The program displays the elements of a vector that holds a hero’s inventory by using returned references. Then the program changes one of the items through a returned reference. Figure 6.4 shows the results of the program.

![](img/34f09be0ed6217c465debc4490197d4f_221_0.png)

### Figure 6.4

The items in the hero’s inventory are displayed and changed by using returned references.

You can download the code for this program from the Course Technology website (www.courseptr.com/downloads). The program is in the Chapter 6 folder; the filename is inventory_referencer.cpp.

```
// Inventory Referencer
// Demonstrates returning a reference

#include <iostream>
#include <string>
#include <vector>

using namespace std;

//returns a reference to a string
string& refToElement(vector<string>& inventory, int i);
```

```
int main()
{
    vector<string> inventory;
    inventory.push_back("sword");
    inventory.push_back("armor");
    inventory.push_back("shield");

    //displays string that the returned reference refers to
    cout << "Sending the returned reference to cout:\n";
    cout << refToElement(inventory, 0) << "\n\n";

    //assigns one reference to another -- inexpensive assignment
    cout << "Assigning the returned reference to another reference.\n";
    string& rStr = refToElement(inventory, 1);
    cout << "Sending the new reference to cout:\n";
    cout << rStr << "\n\n";

    //copies a string object -- expensive assignment
    cout << "Assigning the returned reference to a string object.\n";
    string str = refToElement(inventory, 2);
    cout << "Sending the new string object to cout:\n";
    cout << str << "\n\n";

    //altering the string object through a returned reference
    cout << "Altering an object through a returned reference.\n";
    rStr = "Healing Potion";
    cout << "Sending the altered object to cout:\n";
    cout << inventory[1] << endl;

    return 0;
}

//returns a reference to a string
string& refToElement(vector<string>& vec, int i)
{
    return vec[i];
}
```

## Returning a Reference

Before you can return a reference from a function, you must specify that you’re returning one. That’s what I do in the refToElement() function header.

```
string& refToElement(vector<string>& inventory, int i)
```

By using the reference operator in `string&` when I specify the return type, I’m saying that the function will return a reference to a string object (not a string object itself). You can use the reference operator like I did to specify that a function returns a reference to an object of a particular type. Simply put the reference operator after the type name.

The body of the function `refToElement()` contains only one statement, which returns a reference to the element at position i in the vector.

```
return vec[i];
```

Notice that there’s nothing in the `return` statement to indicate that the function returns a reference. The function header and prototype determine whether a function returns an object or a reference to an object.

## Trap

Although returning a reference can be an efficient way to send information back to a calling function, you have to be careful not to return a reference to an out-of-scope object—an object that ceases to exist. For example, the following function returns a reference to a `string` object that no longer exists after the function ends—and that’s illegal.

```
string& badReference()
{
    string local = "This string will cease to exist once the function ends.";
    return local;
}
```

One way to avoid this type of problem is to never return a reference to a local variable.

## Displaying the Value of a Returned Reference

After creating `inventory`, a vector of items, I display the first item through a returned reference.

```
cout << refToElement(inventory, 0) << "\n\n";
```

The preceding code calls `refToElement()`, which returns a reference to the element at position 0 of `inventory` and then sends that reference to `cout`. As a result, `sword` is displayed.

## Assigning a Returned Reference to a Reference

Next I assign a returned reference to another reference with the following line, which takes a reference to the element in position 1 of `inventory` and assigns it to `rStr`.

```
string& rStr = refToElement(inventory, 1);
```

This is an efficient assignment because assigning a reference to a reference does not involve the copying of an object. Then I send `rStr` to `cout`, and armor is displayed.

## Assigning a Returned Reference to a Variable

Next I assign a returned reference to a variable.

```
string str = refToElement(inventory, 2);
```

The preceding code doesn’t assign a reference to `str`. It can’t, because `str` is a `string` object. Instead, the code copies the element to which the returned reference refers (the element in position 2 of `inventory`) and assigns that new copy of the `string` object to `str`. Because this kind of assignment involves copying an object, it’s more expensive than assigning one reference to another. Sometimes the cost of copying an object this way is perfectly acceptable, but you should be aware of the extra overhead associated with this kind of assignment and avoid it when necessary.

Next I send the new `string` object, `str`, to `cout`, and shield is displayed.

## Altering an Object through a Returned Reference

You can also alter the object to which a returned reference refers. This means you can change the hero’s inventory through `rStr`, as in the following line of code.

```
rStr = "Healing Potion";
```

Because `rStr` refers to the element in position 1 of `inventory`, this code changes `inventory[1]` so it’s equal to "Healing Potion". To prove it, I display the element using the following line, which does indeed show `Healing Potion`.

```
cout << inventory[1] << endl;
```

If I want to protect `inventory` so a reference returned by `refToElement()` can’t be used to change the vector, I should specify the return type of the function as a constant reference.
