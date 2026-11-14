If we tried to access the wrong type or index, e.g.:

```
int i = get<int>(var); // Error at run time
```

an exception of type `bad_variant_access` is thrown.

The special charm of `variant` shows up when we refrain from explicitly dispatching between the possible types of the values and leave this to function overloading. Assume we have a container of our `variant` type and we like to count how many objects of each possible value type are stored, and for no specific reasons we like to guess how many symbols would be written to a stream if we printed the entire container (we know there are simpler ways to do this). We first create a simplistic `record` class:

```
struct record
{
    int counted_ints= 0,
           counted_doubles= 0,
           counted_strings= 0,
           total_symbols= 0;
};
```

Then we create a functor `symbol_counter` that refers the `record` and overloads the application operator for our value types:

Click here to view code image

```
struct symbol_counter
{
    symbol_counter(record& r) : r(r) {}

    void operator()(int i) const
    {
        r.counted_ints++;
        r.total_symbols+= floor(log10(i)) + 1;
    }

    void operator()(double d) const
    {
        r.counted_doubles ++;
        r.total_symbols+= 15;
    }

    void operator()(const string & s) const
    {
        r.counted_strings++;
        r.total_symbols+= s. size();
    }
}
```