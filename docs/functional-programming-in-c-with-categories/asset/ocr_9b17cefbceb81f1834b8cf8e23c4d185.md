![](bbox=[0.26, 0.09, 0.73, 0.32])

We can create a new predicate, by just applying both predicates and then gluing their bool results.

Then we can use some elementary basic predicates on the product :

```
Func<string, Func<Product, bool>> nameContains = pattern => product =>
    product.Name.Contains(pattern);
```

```
Func<Product, bool> highPriced = product => product.Price > 1000;
```

and then we can compose them using And, Or, and Not to create more complex predicates like :

```
Func<Product, bool> highPricedAndContaisA = And(highPriced, nameContains("A"));
```

we can use those predicates with the filter method of the array :

```
var products = new List<Product>{
    new Product("widgetA",100 ),
    new Product( "widgetB",1100),
    new Product( "widgetA",2000),
    new Product( "widgetB",300)
};
```

```
var notHighPricedAndContaisA = Not(highPricedAndContaisA);
```

```
var filiteredProducts = products.Where(notHighPricedAndContaisA);
```

Run This: .Net Fiddle

or try filtering the List with the following Predicates

```
var filter = Or(highPriced, nameContains("B"));
```

```
var filter = Not(Or(highPriced, nameContains("B")));
```