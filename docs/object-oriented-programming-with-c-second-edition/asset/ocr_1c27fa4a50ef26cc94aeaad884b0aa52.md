Number of occurrences of Anand: 0
Number of games of Anand is: 0
Number of occurrences of Anand is: 1
Number of occurrences of Tendulkar is: 0
Tendulkar not found
Number of occurrences of Tendulkar is: 0

# 10.4.5 set Class

The set class is used to create sequential containers. Elements of the list are single objects. A set stores a collection of keys in a sorted manner. The data itself serves as the keys of the set. The set contains the elements in a sorted fashion and duplicates are discarded during insertion.

For using the set template, the header file set needs be included in the source code.

```
#include<set>
```

An illustrative program follows in Listing 10.24.

| Listing 10.24 The set class |
| /*Beginning of set.cpp*/ |
| #include<set> |
| #include<string> |
| #include<iostream.h> |
| void main() {
| set<char> set1; //a set of characters
| string s1("I am indeed a cat. This is indeed a hat");
| cout<<s1<<endl;
| //Putting all the characters of the string s1 in
| //set. Characters get automatically sorted while
| //duplicates get automatically rejected
| set1.insert(s1.begin(),s1.end());
| set<char)::iterator iter;
| for(iter= set1.begin(); iter!=set1.end(); iter++) {
| cout <<*iter; //outputting the set
} 
| /*End of set.cpp*/ |

Output
Iam indeed a cat. This is indeed a hat
Itacdehimnst

# 10.4.6 multimap Class class

The only difference between the map and the multimap class is that while the map class does not allow duplicate key values (it overrides the old value associated with a key), the multimap