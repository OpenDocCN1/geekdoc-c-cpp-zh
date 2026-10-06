# 10.4 Algorithms in STL 435

```
//Find a sub-interval in an ordered interval, make sure all
//elements in the sub-interval are equal to a specified value
pair<vector<int>::iterator, vector<int>::iterator> pairIter;
pairIter=equal_range(vector2.begin(),vector2.end(),22);
out<<(pairIter.first)<<endl;
cout<<(pairIter.second)<<endl;
```

```
//Merge 2 ordered sequences and replace the original sequences
int iarray3[] = { 1, 3, 5, 7, 2, 4, 6, 8 };
vector<int> ivector3(iarray3,iarray3+sizeof(iarray)/sizeof(iarray));
inplace_merge(ivector3.begin(), ivector3.begin()+ 4,
ivector3.end());
copy(ivector3.begin(),ivector3.end(), ostream_iterator<int>
cout << " \nendl;
```

```
//Compare vector3 and vector4 in lexicographical way
int iarray4[] = { 1, 3, 5, 7, 1, 5, 9, 3 };
vector<int> ivector4(iarray4,iarray4+sizeof(iarray)/sizeof(iarray));
out<< lexicographical_compare(ivector3.begin(),ivector3.end(),
ivector4.begin(),ivector4.end()) << endl;
```

Results:

40
15
15 17 22 26 23 33 32 40
15 17 22 23 26
15 17 22 26 23 33 32 40
26
26
1
0
15 17 22 26 23 32 33 40
15 17 22 26 23 32 33 40
15 15 17 17 22 22 23 23 26 26 32 33 40
15 15 17 17 22 22 23 23 26 26 32 33 40
15 15 17 17 22 22 23 23 26 26 32 33 40
22
23
1 2 3 4 5 6 7 8
1