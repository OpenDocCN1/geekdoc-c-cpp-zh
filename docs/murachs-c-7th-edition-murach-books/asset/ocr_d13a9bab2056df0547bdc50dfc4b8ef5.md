# The code for a simple ProductList class

```
public class ProductList
{
    private List<Product> products;

    public ProductList()
    {
        products = new List<Product>();
    }

    public int Count => products.Count;

    public void Add(Product product)
    {
        products.Add(product);
    }

    public void Add(string code, string description, decimal price)
    {
        Product p = new Product(code, description, price);
        products.Add(p);
    }

    public Product GetProductByIndex(int i) => products[i];

    public void Remove(Product product)
    {
        products.Remove(product);
    }

    public void Fill() => products = ProductDB.GetProducts();

    public void Save() => ProductDB.SaveProducts(products);
}
```