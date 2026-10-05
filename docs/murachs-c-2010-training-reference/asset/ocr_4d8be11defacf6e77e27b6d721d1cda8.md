# The code for a simple ProductList class

```
public class ProductList
{
    private List<Product> products;

    public ProductList()
    {
        products = new List<Product>();
    }

    public int Count
    {
        get { return products.Count; }
    }

    public void Add(Product product)
    {
        products.Add(product);
    }

    public void Add(string code, string description, decimal price)
    {
        Product p = new Product(code, description, price);
        products.Add(p);
    }

    public Product GetByIndex(int i)
    {
        return products[i];
    }

    public void Remove(Product product)
    {
        products.Remove(product);
    }

    public void Fill()
    {
        products = ProductDB.GetProducts();
    }

    public void Save()
    {
        ProductDB.SaveProducts(products);
    }
}
```

Figure 13-1 The code for a simple ProductList class