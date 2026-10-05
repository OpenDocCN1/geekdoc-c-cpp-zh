```
p erase += 2;

// insert 10 X's into v
v.insert(p, 10, 'X');

// display contents after insertion X's = "ncout << "Size after inserting X's = " << v.size() << endl;
cout << "Vector contents after insertion:\n"
for(int i = 0; i < v.size(); i++) cout << v[i] << " ";
cout << "\n";

// remove the inserted elements
p = v.begin();
                       // point to 3rd element
p += 2;
// remove next 10 elements
v.erase(p, p+10);

// display contents after deletion "
cout << "Vector size after erase = " << v.size() << endl;
cout << "Vector contents after erase:\n"
for (int i = 0; i < v.size(); i++) cout << v[i] << " ";
cout << "\n";

// Insert v2 into v
v.insert(p, v.begin(), v2.end());

cout << "Size after v2's insertion into v = "
cout << v.size() << endl;
cout << "Contents of vector after insertion:\n"

for (int i = 0; i < v.size(); i++) cout << v[i] << " ";
cout << endl;
return 0;
}

Output:
Original contents of v:
a a a a a a a a a

Size after inserting X's = 20
Vector contents after insertion:
a a X X X X X X X X a a a a a a a a

Size after erase = 10
Vector contents after erase:
a a a a a a a a a a
Size after v2's insertion into v = 18
Contents of vector after insertion:
a a <Vector> a a a a a a a a
```