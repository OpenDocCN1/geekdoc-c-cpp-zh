```
```
        int c;
    void add(base_class rd){
    c = rd.a+ rd.b;
    cout << "\n" << c;
    }
    };
    int main ()
    {
int cont;
base_class rd;
friend_class rs;
rd.read_input();
rs.add(rd);
getchar ();
return 0;
    }
```
```

+   (a) Compilation error
+   (b) 15
+   (c) 10
+   (d) No output and no error

**Answer: (b)** Since the data members a and b are public, no access restrictions would be imposed and the code will work fine. There is no need for someone to use the friend class as well in this case.

# 13. What is the output of the following code snippet? (L3)

```
```
    #include <iostream>
    using namespace std;
    class base_class{
protected:
    int a,b;
    void read_input ()
    {
      a = 5;
      b = 10;
    }
};
   class friend_class{
public:
```
```

```
```
        int c;
    void add(base_class rd){
        c = rd.a+ rd.b;
        cout << "\n" << c;
    }
    };
    int main ()
    {
int cont;
base_class rd;
friend_class rs;
rd.read_input();
rs.add(rd);
getchar ();
return 0;
    }
```
```

+   (a) Compilation error
+   (b) 15
+   (c) 10
+   (d) No output and no error

**Answer: (a)** Protected is the access specifier used in this scenario hence, the data members of the base class are accessible only by its derived class. Hence, it would result in compilation fault.

# 14. What is the output of the below code snippet? (L4)

```
```
    #include <iostream>
    using namespace std;
    class base_class{
protected:
    int a, b;
public:
    int d;
    void read_input ()
    {
      a = 5;
      b = 10;
      d = 10;
```
```