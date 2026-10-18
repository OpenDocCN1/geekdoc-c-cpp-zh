![](bbox=[0.3221, 0.0852, 0.6758, 0.3825])

The program illustrates that the objects of class D have access to all the public members of B. Let us have a look at the functions show_a() and mul():

```
void show_a()
{
cout << "a = " << a << "\n";
}
void mul()
{
c = b * get_a();// c = b * a
}
```

Although the data member a is private in B and cannot be inherited, objects of D are able to access it through an inherited member function of B.

Let us now consider the case of private derivation.

+   class B
+   {