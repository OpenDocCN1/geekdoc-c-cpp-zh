```
```cpp
72        firstPtr = newPtr; // aim firstPtr at new node
73    } // end else
74 } // end function insertAtFront
75
76 // insert node at back of list
77 template< typename NODETYPE >
78 void List< NODETYPE >::insertAtBack( const NODETYPE &value )
79 {
80    ListNode< NODETYPE > *newPtr = getNewNode( value ); // new node
81
82    if ( isEmpty() ) // List is empty
83       firstPtr = lastPtr = newPtr; // new list has only one node
84    else // List is not empty
85    {
86       lastPtr->nextPtr = newPtr; // update previous last node
87       lastPtr = newPtr; // new last node
88    } // end else
89 } // end function insertAtBack
90
91 // delete node from front of list
92 template< typename NODETYPE >
93 bool List< NODETYPE >::removeFromFront( NODETYPE &value )
94 {
95    if ( isEmpty() ) // List is empty
96       return false; // delete unsuccessful
97    else
98    {
99       ListNode< NODETYPE > *tempPtr = firstPtr; // hold tempPtr to delete
100
101      if ( firstPtr == lastPtr )
102         firstPtr = lastPtr = 0; // no nodes remain after removal
103      else
104         firstPtr = firstPtr->nextPtr; // point to previous 2nd node
105
106      value = tempPtr->data; // return data being removed
107      delete tempPtr; // reclaim previous front node
108      return true; // delete successful
109   } // end else
110 } // end function removeFromFront
111
112 // delete node from back of list
113 template< typename NODETYPE >
114 bool List< NODETYPE >::removeFromBack( NODETYPE &value )
115 {
116    if ( isEmpty() ) // List is empty
117       return false; // delete unsuccessful
118    else
119    {
120       ListNode< NODETYPE > *tempPtr = lastPtr; // hold tempPtr to delete
121
122      if ( firstPtr == lastPtr ) // List has one element
123         firstPtr = lastPtr = 0; // no nodes remain after removal
```
```

Fig. 20.4 | List class-template definition. (Part 3 of 5.)