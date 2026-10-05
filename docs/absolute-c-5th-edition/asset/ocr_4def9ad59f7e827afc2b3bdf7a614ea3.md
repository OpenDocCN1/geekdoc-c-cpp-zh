# 788 CHAPTER 17 Linked Data Structures

Display 17.29 Implementation File for a Set Template Class (part of 2)

```
41  cout << endl;
42  }
43  template<class T>
44  void Set<T>::add(T item)
45  {
46      if (search(head, item)==NULL)
47      {
48          // add the target if it's not in the list
49          headInserts(head, item);
50      }
51  }
52  template<class T>
53  Set<T>* Set<T>::setUnion(const Set<T>& otherSet)
54  {
55      Set<T> *unionSet = new Set<T>();
56      Node<T>* iterator = head;
57      while (iterator != NULL)
58      {
59          unionSet->add(iterator->getData());
60          iterator = iterator->getLink();
61      }
62      iterator = otherSet.head;
63      while (iterator != NULL)
64      {
65          unionSet->add(iterator->getData());
66          iterator = iterator->getLink();
67      }
68      return unionSet;
69  }
70  template<class T>
71  Set<T>* Set<T>::setIntersection(const Set<T>& otherSet)
72  {
73      Set<T>* *interSet = new Set<T>();
74      Node<T>* iterator = head;
75      while (iterator != NULL)
76      {
77          if (otherSet.contains(iterator->getData()))
78          {
79              interSet->add(iterator->getData());
80          }
81          iterator = iterator->getLink();
82      }\n83      return interSet;
84  }
85  //SetSavitch *
```