61. What is the output of the code? (L3)

```
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m;
        class subject
        { public:
            char grade; };
    }S;
    int main()
    { S.subject sb;
      sb.grade= 'A';
      cout<<sb.grade; }
```

(a) A        (b) Unpredictable
(c) Error    (d) None of the above

Answer: (c) This is not a legal way of creating objects for class that is inside other classes.

62. What will be the error thrown by the code? (L4)

```
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m;
        class subject
        { public:
            char grade; };
    }S;
    int main()
    { S.subject sb;
      sb.grade= 'A';
      cout<<sb.grade; }
```

(a) 'sb' was not declared in this scope
(b) Expected ';' before 'sb'
(c) Invalid use of 'class student::subject'
(d) Both 'a' and 'b'
(e) 'a','b' and 'c'

Answer: (e) Objects for classes defined inside other classes cannot be created outside the outer class.

63. What will be the error thrown by the code? (L4)

```
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m;
        class student
        { public:
            char grade; };sb;
    }S;
    int main()
    { S.m=9;
      cout<<S.m; }
```

(a) Redeclaration of 'class student'
(b) 'class student' incomplete
(c) Invalid use of constructor
(d) 'student::student' has the same name as the class in which it is declared
(e) No error

Answer: (d) class inside a class with same name is not possible.

64. What will be a part of the error thrown by the code? (L4)

```
    #include<iostream>
    using namespace std;
    class student
    { public:
        int m; }S;
    class student
    { public:
        char grade; };sb;
    int main()
    { S.m=9;
      cout<<S.m; }
```

(a) Redeclaration of 'class student'
(b) Redefinition of 'class student'