What we’ve done here is specified what access level the indexer has – we used public – and then specified the return type. The ‘this’ keyword is used with the [] square brackets used to indicate indexing. In the square brackets, we put the indexing variable type and name that is going to be used in the indexer.

Then, in much the same way as we do with a property, we have our blocks of get and set code. Again like a property, you don’t have to use both if you don’t want or need to – just stick with one. Inside of these blocks, the variable called index can be used along with the value keyword inside the setter referencing the value that will be assigned.

In this example, I have made it so that the x and y components of the vector can be referenced by others using the 0 index for x and the 1 index for y. With all of that, we can now do this:

```
Vector v = new Vector(5, 2);
```

```
double xComponent = v[0]; // Now we can use the indexing operator.
```

```
double yComponent = v[1];
```

This is a good deal easier to read and understand than the alternative would be – that would have had a method called GetIndex, or something like it and would have read xComponent = v.GetIndex(0);.

But you don’t just have to use an ints for your index. You could also use doubles, strings, or anything else that you want. In fact, think about when we talked about generics; the Dictionary class does just that.

This example shows you how to do indexing with strings:

```
public double this[string component]
{
    get
    {
```