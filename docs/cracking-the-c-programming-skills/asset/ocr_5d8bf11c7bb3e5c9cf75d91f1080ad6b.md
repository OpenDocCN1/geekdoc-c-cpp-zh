(a) 4 (b) 0
(c) Unpredictable (d) None of the above
Answer: (a) Even though the members are not accessible by the object, each object will have a specific value of the variable. So it will be allocated.

9. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class student
{ protected:
  int marks;
  void percent()
  { cout<< marks*10; }
};
int main()
{ cout<<sizeof(S) ; }
```

(a) 4 (b) 0
(c) Unpredictable (d) None of the above
Answer: (a) The same here.

10. What is the output of the code? (L1)

```cpp
#include<iostream>
using namespace std;
class student
{ char section;
public:
  int marks;
  void percent()
  { cout<< marks*10; }
};
int main()
{ cout<<sizeof(S) ; }
```

(a) 4 (b) 5
(c) Unpredictable (d) None of the above
Answer: (b) This works normally.

11. What is the output of the code? (L1)

```cpp
#include<iostream>
using namespace std;
class student
```

```cpp
{ public:
  int marks;
  char section;
}S;
int main()
{ S.marks=8;
  S.section = 'a';
  cout<<S.marks<< " " <<S.section;
}
```

(a) 8 a (b) Unpredictable
(c) Error (d) None of the above
Answer: (a) Unnecessary blank lines within the 'class' doesn't change the specifiers to default ('private').

12. What is the output of the code? (L2)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
  int marks;
private:
  char section;
}S;
int main()
{ S.marks=8;
  S.section = 'a';
  cout<<S.marks<< " " <<S.section; }
```

(a) 8 a (b) Unpredictable
(c) Error (d) None of the above
Answer: (c) This works exactly as expected.

13. What is the output of the code? (L3)

```cpp
#include<iostream>
using namespace std;
class student
{ public:
  int marks;
private:
  int m;
public:
  char section;
```