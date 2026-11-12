(a) 234    (b) 230
(c) Unpredictable    (d) None of the above

**Answer:** (a) When data of different types is given, it internally converts it into the required type and saves it.

25. What is the output of the code? (assume the values given are 2,2,3,4,34) (L3)

```
    #include<iostream>
    using namespace std;
    int main()
    { int a,b,c;
  cin>>a>>b>>c;
  cout<< a;
  cout<< b;
  cout<< c;  }
```

(a) 234    (b) 230
(c) Unpredictable    (d) None of the above

**Answer:** (d) 200 is the output. 'cin' stops reading the value when it encounters a mismatch in type.

26. What is the output of the code? (assume the values given are 2,2,3,4,34) (L3)

```
    #include<iostream>
    using namespace std;
    int main()
    { int a,b,c;
  cin>>a;
  cin>>b;
  cin>>c;
  cout<< a;
     cout<< b;
     cout<< c;  }
```

(a) 200    (b) 234
(c) Unpredictable    (d) None of the above

**Answer:** (a) This also works in the same way. When one 'cin' fails all the others are skipped.

27. What is the output of the code? (assume the values given are 2,2,3,4,34) (L3)

```
    #include<iostream>
    using namespace std;
    int main()
    { int a,b,c;
  cin>>a;
  cin>>b;
  cin>>c;
  cout<< int(a);
  cout<< b;
  cout<< int(c);  }
```

(a) 200    (b) 234
(c) Unpredictable    (d) None of the above

**Answer:** (a) This also works the same as above. But the conversion has no issues, it is all the same as 'C'.

28. What is the output of the code? (assume the values given are 2,2,3,4,34) (L4)

```
    #include<iostream>
    using namespace std;
    int main()
    { int a,b,c;
  cin>>int(a);
  cin>>b;
  cin>>int(c);
      cout<< a;
      cout<< b;
      cout<< c;  }
```

(a) 200    (b) 234
(c) Unpredictable    (d) None of the above

**Answer:** (d) This gives error. "Ambiguous overload for 'operator>>'". It gives a long description of the internal definition of the operator and the possible overloading of it. Overloading is a concept of object oriented programming which means giving multiple definitions for an operator based on usage.