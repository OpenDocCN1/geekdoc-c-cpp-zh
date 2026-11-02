You may need to clear the counter, for example at the end of a sale or a statement period.

```
```cpp
void clear()
{
    total_price = 0;
    item_count = 0;
}
```
```

There may or may not be a member function that reports the count to the class user. The count may only be used to compute a fee or an average. Find out which member functions in your class make use of the count, and read the current value in those member functions.

# 9.11.3 Collecting Values

Some objects collect numbers, strings, or other objects. For example, each multiple-choice question has a number of choices. A cash register may need to store all prices of the current sale.

![](bbox=[0.72, 0.38, 0.92, 0.65])

An object can collect other objects in an array or vector.

Use a vector or an array to store the values. (A vector is usually simpler because you won't need to track the number of values.) For example,

```
```cpp
class Question
{
...
private:
    vector<string> choices;
...
};
```
```

In the constructor, we want to initialize the data member to an empty collection. The default constructor of the vector class does that automatically. Therefore, the constructor has no explicit actions:

```
```cpp
Question::Question()
{
}
```
```

You need to supply some mechanism for adding values. It is common to provide a member function for appending a value to the collection:

```
```cpp
void Question::add(string choice)
{
    choices.push_back(choice);
}
```
```

The user of a Question object can call this member function multiple times to add the various choices.

# 9.11.4 Managing Properties of an Object

A property is a value of an object that an object user can set and retrieve. For example, a Student object may have a name and an ID.