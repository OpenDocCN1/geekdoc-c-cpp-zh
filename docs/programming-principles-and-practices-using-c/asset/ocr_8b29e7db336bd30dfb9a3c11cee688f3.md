Iterating through a map is easy. We just have to remember that the key is called **first** and the value is called **second**:

```
```c++
// write price for each company in the Dow index:
for (const auto& p : dow_price) {
  const string& symbol = p.first;       // the “ticker” symbol
  cout << symbol << ‘'’
       << p.second << ‘'’
       << dow_name[symbol] << ‘\n’;
}
```
```

We can even do some computation directly using maps. In particular, we can calculate the index, just as we did in §21.5.3. We have to extract share values and weights from their respective maps and multiply them. We can easily write a function for doing that for any two **map<string,double>**s:

```
```c++
double weighted_value(
  const pair<string,double>&& a,
  const pair<string,double>&& b
)  // extract values and multiply
{
  return a.second * b.second;
}
```
```

Now we just plug that function into the generalized version of **inner_product()** and we have the value of our index:

```
```c++
double dji_index =
  inner_product(dow_price.begin(), dow_price.end(),    // all companies
                dow_weight.begin(),                   // their weights
                0.0,                                  // initial value
                plus<double>(),                        // add (as usual)
                weighted_value);                       // extract values and weights
                                                       // and multiply
```
```

Why might someone keep such data in **maps** rather than **vectors**? We used a **map** to make the association between the different values explicit. That’s one common reason. Another is that a **map** keeps its elements in the order defined by its key. When we iterated through **dow** above, we output the symbols in alphabetical order; had we used a **vector** we would have had to sort. The most common reason to use a **map** is simply that we want to look up values based on the key. For large