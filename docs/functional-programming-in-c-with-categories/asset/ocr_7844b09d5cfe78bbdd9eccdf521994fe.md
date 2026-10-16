Let us start with simple example where we have a ProductA, and we can decorate it with Packaging. Adding a packaging would affect the price, but we want to treat a product and a packaged product interchangeably in our code. The decorator pattern allows us to do just that by unifying both ProductA and Packaging under a common IPriced interface :

```
public interface IPriced {
  double GetPrice();
}
```

```
public class ProductA : IPriced {
  public double GetPrice() => 100;
}
```

```
public class Packaging : IPriced
{
  private readonly IPriced product;
  public Packaging(IPriced product) => this.product = product;
  public double GetPrice() => product.GetPrice() + 10;
}
```

![](bbox=[0.45, 0.25, 0.95, 0.55])

The decorator pattern is based on the idea/theme that the decorator exposes the same interface with the decorated object.

In this example, the Packaging exposes the same GetPrice() method with the decorated Product. This allows the rest of the application to handle a simple product or a decorated product in the same way without needing to know more details in order to get the price [this is a nice display of information hiding/encapsulation in object-oriented programming, since the decorated object hides the details of implementation from the outside world and only reveals the price].

From the Functional perspective this again is possible because the + monoid on the return type of the GetPrice function.



Finally, we can strip of all the object-syntax completely and only keep the functions.