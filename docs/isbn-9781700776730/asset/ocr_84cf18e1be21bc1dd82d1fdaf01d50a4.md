```
class Employee {
private:
    const long ssnum;
public:
    Employee(long n) : ssnum(n) {}
};
```

+   - a reference data member

```
class Employee{
private:
    const long ssnum;
    int& value;
public:
    Employee(long n, int val) : ssnum(n), value(val) {}
};
```