# 882 CHAPTER 19 Standard Template Library

Display 19.10 Program Using the stack Template Class (part 2 of 2)

```
while (next != '\n')
{
    s.push(next);
    cin.get(next);
}
```

```
cout << "Written backward that is:";
while (!s.empty())
{
    cout << s.top();
    s.pop();
}
cout << endl;
```

```
return 0;
}
```

Sample Dialogue

```
Enter a line of text:
straw
Written backward that is:
warts
```

# The Associative Containers set and map

Associative containers are basically simple databases. They store data, such as structs or any other type of data. Each data item has an associated value known as its key. For example, if the data is a struct with an employee's record, the key might be the employee's Social Security number. Items are retrieved from the basis of the key. The key type and the type for data to be stored do not have any relationship to one another, although they are often related. A simple case is in a set, every element is its own key.

The set template class is, in some sense, the simplest container you can imagine. It stores elements without repetition. The first insertion places an element in the set so that no element appears more than once. Each element is its own key. Basically, you just add or delete elements and ask if an element is in the set or not. Like all STL classes, the set template class was written with efficiency as a goal. To work efficiently, a set template stores its values in sorted order. You can specify the order for storing elements as follows:

```
set<T, Ordering> s;
```