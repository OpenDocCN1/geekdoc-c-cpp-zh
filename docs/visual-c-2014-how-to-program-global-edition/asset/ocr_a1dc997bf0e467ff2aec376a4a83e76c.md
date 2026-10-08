# 19.4 Linked Lists

```
81  throw new EmptyListException(name);
82  }
83
84  object removeItem = firstNode.Data; // retrieve data
85
86  // reset firstNode and lastNode references
87  if (firstNode == lastNode)
88  {
89      firstNode = null;
90  }
91  else
92  {
93      firstNode = firstNode.Next;
94  }
95
96  return removeItem; // return removed data
97  }
98
99  // remove last node from List
100 public object RemoveBack() {
101\1102if (IsEmpty())
103    {
104      throw new EmptyListException(name);
105    }
106
107  object removeItem = lastNode.Data; // retrieve data
108
109  // reset firstNode and lastNode references
110  if (firstNode == lastNode)
111  {
112      firstNode = lastNode = null;
113  }
114  else
115  {
116      ListNode current = firstNode;
117      // loop while current.Next is not lastNode
118      while (current.Next != null)
119      {
120          current = current.Next; // move to next node
121      }
122      
123      // current is new lastNode
124      lastNode = current;
125      current.Next = null;
126  }
127  }
128
129  return removeItem; // return removed data
130  }
131else
```

Fig. 19.4 | ListNode. List and EmptyListException class declarations. (Part 3 of 4.)