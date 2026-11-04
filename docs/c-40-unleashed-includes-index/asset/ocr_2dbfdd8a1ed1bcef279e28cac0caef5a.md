```
public override string ToString()
{
    return _name + " is " + this._age;
}
}
```

You'll learn what the override modifier on a method means in Chapter 14. It's also essential to realize that the private access modifier doesn't prevent you from accessing another instance's private fields as long as that access happens within code defined on the type. To clarify this, consider the following code, which implements an equality check operation for Person instances:

```
class Person
{
    private string _name;
    private int _age;

    public override bool Equals(object obj)
    {
        if (obj == null || obj.GetType() != this.GetType())
            return false;

        var other = (Person)obj;
        return other._name == this._name && other._age == this._age;
    }
}
```

Implementing a correct Equals override is discussed in Chapter 13, “Operator Overloading and Conversions,” when we discuss operator overloading. The essence is quite simple, though. First we make sure the object passed to us for comparison is of the same type. Instead of using is or as (which produce a positive result when subtyping is involved), we perform an exact match on the System.Type returned by GetType. In addition, we also have to make sure we're not asked to compare with the null reference because null is never equal to an instance. When we know we're comparing existent apples to apples (well, in this case, people), we simply compare the fields pairwise. This illustrates that code declared within the Person type can access the private members of any instance of that Person type.

Static fields are qualified by the type of the containing type. Except for static read-only fields (covered later in this chapter), it shouldn't be the case that such fields are being accessed from outside the containing type. If that holds true, type qualification can be omitted:

```
class Person
{
    private static int s_population;
    private string _name;
    private int _age;
```