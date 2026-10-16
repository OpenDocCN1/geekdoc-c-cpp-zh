We can form products using the available C# syntax in many ways, the following are products or arity-2 formed by two objects (arity is the number of items) but there can be products of any size

```
(int A, int B) product = (A: 10, B: 20); //tuples are products.
```

```
public class Product
{
    public int A { get; set; }
    public int B { get; set; }
}
//objects are products.
```

```
var product = new List<int> { 10, 20 }; //a list can be seen as a product.
```

All those are isomorphic, containing the exact same information, and we could construct functions that convert the one to the other.

That is why we can replace for example the argument list on a method with a Tuple or an object. The following are all equivalent:

```
public static void GetDiscount(int A, int B) { }
public static void GetDiscount((int A, int B) product) { }
public static void GetDiscount(Product product) { }
```

This transformation commonly called Introduce Parameter Object refactoring move. And it is based on the fact that both (,,,) and Tuples ((,,)) are products. The most important law in order to consider something as a product is that we must be able to write two functions that will take a product and gives us the component parts. Those functions are called projections.

![](bbox=[0.32, 0.605, 0.68, 0.635])

For example, for an array definition of a product [, ] the projections would be:

```
var product = new List<int> { 10, 20 };
Func<List<int>, int> first = p => p[0];
Func<List<int>, int> second = p => p[1];
```

For the Tuple (int A, int B) definition of a product the projections would be:

```
(int A, int B) product = (A: 10, B: 20);
```

```
Func<(int A, int B), int> first = p => p.A;
Func<(int A, int B), int> second = p => p.B;
```