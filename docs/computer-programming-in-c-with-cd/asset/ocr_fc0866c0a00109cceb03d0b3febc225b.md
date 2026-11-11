```
```cpp
int k;
public:
    void setdata2() {
        setdata1(34, 60);
        k = i * j;
    }
    void showall() {
        cout << "k : " << k << "\n";
        showdata();
    }
};
int main()
{
    MyDerived md;
    md.setdata2();                 // public member of MyDerived
    md.showall();                  // public member of MyDerived
    return 0;
}

Output:

k : 2040
i : 34
j : 60
```
```

# ## Multilevel Inheritance

A form of inheritance in which a derived class is inherited from a base class, and the same base class in turn is inherited or derived from another base class is called multilevel inheritance, as shown in Figure 3:

![](bbox=[0.475, 0.613, 0.601, 0.83])

▲ Figure 3: Displaying Multilevel Inheritance