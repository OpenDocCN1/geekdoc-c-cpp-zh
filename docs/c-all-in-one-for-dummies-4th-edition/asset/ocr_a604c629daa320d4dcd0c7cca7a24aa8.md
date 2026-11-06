```
    int main() {
      Base<int> base_int;
      Base<double> base_double;

      Derived<int> derived_int;
      Derived<double> derived_double;

      TestInt(&base_int);
      TestInt(&derived_int);
      TestDouble(&base_double);
      TestDouble(&derived_double);

      //TestDouble(&derived_int);
      return 0;
    }
```

![](bbox=[0.177, 0.407, 0.236, 0.497])

The example has two functions, each taking a different class — and each class based on the first template, called Base. The first takes Base<int> * as a parameter, and the second takes Base<double> * as a parameter. When a function, such as TestInt() or TestDouble(), takes a pointer to a class, it can legally pass a pointer to an instance of a derived class, which means that you can create this variable:

```
    Derived<int> derived_int;
```

You pass this variable to the function that takes a Base<int> and it compiles. That means that Derived<int> is derived from Base<int>. In the same way, Derived<double> is derived from Base<double>. When you run this code, it outputs four numbers: two int values and two double values.

To see how Derived<int> relies on Base<int>, uncomment the line TestDouble(&derived_int). When you do this, and you try to compile the listing, you see this message:

```
    error: cannot convert 'Derived<int>*' to 'Base<double>*' for
    argument '1' to 'void TestDouble(Base<double>*)'
```

The error message says you can't pass a pointer to Derived<int> to a function that takes a pointer to Base<double>. That's because Derived<int> isn't derived from Base<double>.

# Creating Classes with Templates