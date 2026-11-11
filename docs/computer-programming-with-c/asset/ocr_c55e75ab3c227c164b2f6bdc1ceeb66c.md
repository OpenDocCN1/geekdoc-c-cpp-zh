You can only use ++ or -- operators with the iterator of linked list; this is because linked list iterator can only move one step at a time. The statements given in the table above will not work for linked list iterator but will work for a vector iterator.

Given below is the demonstration of random iterator supported by vector. Note that the for loop has an initialization statement as

```
    temp= vl.begin()+5
```

which means that the iteration will start from 6th element of the vector. This means that the first five elements of the vector will not be printed.

```
    #include<vector.h>
    void main()
    {
        vector<int> vl;
        int i;
        for(i=0;i<=10;i++)
        {
            vl.push_back(i);
        }
        cout<<"Printing vector skipping first 5 elements"<<endl;
        vector<int> :: iterator temp;
        for(temp = vl.begin()+5;temp != vl.end() ; temp++)
        {
            cout<<*temp<<" ";
        }
    }
```

# **Output**

```
    Printing vector skipping first 5 elements
    5 6 7 8 9 10
```

# ### 16.4.3 Map

Map is a collection which stores data in the form of key, value pairs. You can imagine a map as a table indexed by key and a specific data value which is stored corresponding to each key. Key must be unique for each entry in the map, however it is possible to have same or different value for two different entries of the map.

For example, consider a map that stores roll number and name of students. Here, roll number is a unique identifier and is a key for each entry. Value is the name of the student. It is realistic that two different students have same name in the real world, however their roll numbers will be different. All this means is that, values can have duplicates but key must be unique.

Given below is the program that demonstrates usage of built-in collection map in C++.