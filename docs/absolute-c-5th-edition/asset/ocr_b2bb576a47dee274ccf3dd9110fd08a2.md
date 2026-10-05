# 796 CHAPTER 17 Linked Data Structures

Display 17.31 An Iterator Class for Linked Lists (part 2 of 2)

```
41    }
42    bool operator ==(const ListIterator& rightSide) const
43    { return (current == rightSide.current); }

44    bool operator !==(const ListIterator& rightSide) const
45    { return (current != rightSide.current); }

46    // The default assignment operator and copy constructor
47    //should work correctly for ListIterator.
48    private:
49    Node<T> *current;
50    };

51 } //ListNodeSavitch
52 #endif ITERATOR_H
```

# EXAMPLE: (continued)

The member function end() returns an iterator whose member variable is NULL. Thus, when the iterator i has passed the last node, the Boolean expression

```
i != q.end()
```

changes from true to false. This is the desired Stopping_Condition. This queue and class iterator allows you to cycle through the data in the queue in the way we outlined for iterator:

```
for (i = q.begin(); i != q.end(); i++)
    process //* i is the current data item.
```

Note that i is not equal to q.end() when i is at the last node. The iterator i is not equal to q.end() until it has advanced once position past the last node. To remember this detail, think of q.end() as being an end marker like NULL; in this case, it is essentially a version of NULL. A sample program that uses such a for loop is shown in Display 17.33.

Notice the type definition in our new queue template:

```
typedef ListIterator<T> Iterator;
```

(continued on page 799)