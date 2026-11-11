```
*/

cout << " Thus,\t\t*it = " << *it << " that is data[0]\n Iterators can be incremented, i,e, ++it;\n";

++it;

cout << " After ++\t*it = " << *it << " that is data[1]\n Therefore, iterator *it dereferences through vector data.\n So, let us express the entire vector using the iterator:  \n\t( ";
for(auto it = data.begin(); it!=data.end(); ++it)
    cout << *it << "; ";
cout << ")\n";

cout << "\n Task: Since, this vector has repeated numbers,\n Can we keep only one copy of each number and remove the duplicates?\n Yes, we can!\n For that, we pass the iterator through three type of STL algorithms as shown below:\n";

cout << "\n Step.1 Sort in ascending order:\n";
sort(data.begin(), data.end());

cout << " After the iterator has passed through sort(): \n\t( ";
for(auto element: data)
    cout << element << "; ";
cout << ")\n\n Step.2 Move the adjacent repeated elements to the left hand side:\n";

auto my_unique = unique(data.begin(), data.end());

cout << " After the iterator has passed through unique(): \n\t( ";
for(auto element: data)
    cout << element << "; ";

/*
```