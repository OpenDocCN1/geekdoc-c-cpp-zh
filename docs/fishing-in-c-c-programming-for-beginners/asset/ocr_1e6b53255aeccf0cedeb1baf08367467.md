```
Counter operator+(const Counter &);
private:
USHORT itsVal;
};
```

```
Counter::Counter(USHORT initialValue):
itsVal(initialValue)
{}
```

```
Counter::Counter():
itsVal(0)
{}
```

```
Counter Counter::operator+ (const Counter & rmo)
{
    return Counter(itsVal + rmo.GetItsVal());
}
```

```
int main()
{
    Counter first(2);
    Counter second=first;
    cout << "second: " << second.GetItsVal() << endl;
    return 0;
}
```

Ouput