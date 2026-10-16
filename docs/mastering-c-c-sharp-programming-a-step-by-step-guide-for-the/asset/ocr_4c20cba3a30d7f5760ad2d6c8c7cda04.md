```
if (component == "x") { return this.X; }
else if (component == "y") { return this.Y; }
else { throw new IndexOutOfRangeException(); }
}
set
{
if (component == "x") { this.X = value; }
else if (component == "y") { this.Y = value; }
else { throw new IndexOutOfRangeException(); }
}
}
```

This is similar to what we used earlier, but we used a string for the indexing instead rather than an int. If x is asked for, the x-component is returned, and if y is asked for, the y-component is returned.

So now we can do this:

```
Vector v = new Vector(5, 2);
double xComponent = v["x"]; // Now we can use the indexing operator.
double yComponent = v["y"];
```

This gets better because we can also index using several indices. Again, you may be able to do it but it doesn’t mean you should. Only do this when it is appropriate to do so.

To add several indices, all you do is list them inside the square brackets where the indexer is defined.

```
public double this[string component, int index]
{
    get
```