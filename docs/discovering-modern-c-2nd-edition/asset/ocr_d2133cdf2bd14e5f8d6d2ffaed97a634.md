terminated their access to it. In contrast to a `unique_ptr`, a `shared_ptr` can be copied as often as desired, e.g.:

Click here to view code image

```
shared_ptr<double> f()
{
    shared_ptr<double> p1(new double);
    shared_ptr<double> p2(new double), p3= p1;
    cout << "p3.use_count() = " << p3.use_count() << endl;
    return p3;
}
```

```
int main ()
{
    shared_ptr<double> p= f());
    cout << "p.use_count() = " << p.use_count() << endl;
}
```

In this example, we allocated memory for two `double` values: in `p1` and in `p2`. The pointer `p1` is copied into `p3` so that both point to the same memory, as illustrated in Figure 1–1.

![](bbox=[0.225, 0.515, 0.73, 0.71])

# Figure 1–1: Shared pointer in memory

We can see this from the output of `use_count`:

Click here to view code image

```
p3.use_count() = 2
p.use_count() = 1
```