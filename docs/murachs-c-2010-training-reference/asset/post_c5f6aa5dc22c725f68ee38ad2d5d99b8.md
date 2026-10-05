
## Chapter 13 How to work with indexers, delegates, events, and operators 411

### Code that overflows the == operator for a Product class

```cs
public static bool operator == (Product p1, Product p2)
{
    if (Object.Equals(p1, null))
    {
        if (Object.Equals(p2, null))
            return true;
        else
            return false;
    }
    else
        return p1.Equals(p2);
}

public static bool operator != (Product p1, Product p2)
{
    return !(p1 == p2);
}
```

```cs
public override bool Equals(Object obj)
{
    if (obj == null)
        return false;
    Product p = (Product)obj;
    if (this.Code == p.Code &&
        this.Description == p.Description &&
        this.Price == p.Price)
        return true;
    else
        return false;
}
```

```cs
public override int GetHashCode()
{
    string hashString = this.Code + this.Description + this.Price;
    return hashString.GetHashCode();
}
```

Code that uses the == operator of the Product class
Product p1 = new Product("CSI10", "Murach's C# 2010", 54.50m);
Product p2 = new Product("CSI10", "Murach's C# 2010", 54.50m);
if (p1 == p2) // This evaluates to true. Without the overloaded
    // operator, it would evaluate to false.

# Description

- If you overload the == operator, you must also override the non-static Equals methods. Then, the == operator should use this Equals method for its equality test.
- Before it calls the Equals method, the overloaded == operator should test the operands for null values. If both operands are null, they should be considered equal. If only the first operand is null, the operands should be considered unequal.
- Relational operators must be implemented in pairs. For example, if you overload the == operator, you must also overload the != operator.
- When you overload the Equals method, you must also override the GetHashCode method. That's because GetHashCode method must return the same hash code for any two instances that are equal by the Equals method.

Figure 13-9 How to overload the == operator

## An enhanced version of the Product Maintenance application

created from the Product class with identical values. Then, the products are compared in an if statement using the == operator. Because both products have the Code, Description, and Price values, this comparison returns true. If the Product class didn't override the == operator, however, this comparison would return false because the p1 and p2 variables refer to different instances of the Product class, even though they have the same values.

Before I go on, you might want to consider why it's necessary for the == operator to be static. If it weren't, you would have to call it from an instance of the Product class, for example, p1. But what if p1 was null? In other words, what if p1 didn't refer to an instance of the Product class? In that case, you couldn't use the == operator. With null operands, then, overloaded operators must be declared as static.

Now that you've learned the techniques for enhancing your classes, the topics that follow present an enhanced version of the Product Maintenance application that uses those enhancements. From the user's standpoint, the application operates like the one that was presented in chapter 12. The only difference is that the classes in this version of the application are implemented differently. Specifically, the ProductList class includes the additional members that are shown in figure 13-2.

Because the code for the Product class is the same as the Product class presented in chapter 12, I won't repeat it here. Similarly, the New Product form that's used in this version of the Product Maintenance application is identical to the code shown in chapter 12. As a result, I won't repeat that code either. Finally, like the application in chapter 12, you should know that this application will work with any of the three versions of the ProductDB class that are presented in 21 and 22.

## The code for the ProductList class

Figure 13-10 shows the code for the ProductList class, which stores a collection of Product objects. To help you follow it, I've highlighted some of the critical statements.

As you can see, this class begins by declaring a List<object> named products. This instance variable is used to store the product list. Next, the ProductList declares a delegate EventHandler and an event named Changed that uses this delegate. This event is raised whenever the contents of the products list are changed.

The two indexers for this class let users of the class to access a specific product in the list by specifying an integer value or a product code. Since these indexers are similar to the two indexers in figure 13-3, you shouldn't have any

### The code for the ProductList class Page 1

```cs
public class ProductList
{
    private List<Product> products;
    public delegate void ChangeNotifier(ProductList products);
    public event EventHandler Changed;

    public ProductList()
    {
        products = new List<Product>();
    }

    public int Count
    {
        get
        {
            return products.Count;
        }
    }

    public Product this[int i]
    {
        get
        {
            if (i < 0)
                throw new ArgumentRangeException(i.ToString());
            else if (i >= products.Count)
                throw new ArgumentOutOfRangeException(i.ToString());
            return products[i];
        }
        set
        {
            products[i] = value;
            Changed(this);
        }
    }

    public Product this[string code]
    {
        get
        {
            foreach (Product p in products)
            {
                if (p.Code == code)
                    return p;
            }
            return null;
        }
    }
}
```

Figure 13-10 The code for the ProductList class (part 1 of 2)

### 414 Section 3 Object-oriented programming

trouble how they work. The main difference is that the set accessor for the first indexer raises the Changed event to indicate that the contents of the products list have changed.

The Fill method of the ProductList class, shown on page 2 of this listing, calls the GetProducts method of the ProductDB class to get the products from a file. Similarly, the Save method calls the SaveProducts method of this class to save the products to a file.

The ProductList class also provides two overloads for the Add method: one that accepts a Product object and one that accepts a code and price. It also includes a Remove method that removes the specified Product object. As you can see, all three of these methods raise the Changed event.

Finally, this class provides an overloaded + operator and an overloaded operator. The overloaded + operator calls the first Add method to add the specified object to the product list and then returns the updated product list. Similarly, the – operator calls the Remove method to remove the specified product from the product list and then returns the updated product list.

### The code for the ProductList class Page 2

```cs
public void Fill()
{
    products = ProductDB.GetProducts();
}

public void Save()
{
    ProductDB.SaveProducts(products);
}
```

```cs
public void Add(Product product)
{
    products.Add(product);
    Changed(this);
}
```

```cs
public void Add(string code, string description, decimal price)
{
    Product p = new Product(code, description, price);
    products.Add(p);
    Changed(this);
}
```

```cs
public void Remove(Product product)
{
    products.Remove(product);
    Changed(this);
}
```

```cs
public static ProductList operator + (ProductList pl, Product p)
{
    pl.Add(p);
    return pl;
}
```

```cs
public static ProductList operator - (ProductList pl, Product p)
{
    pl.Remove(p);
    return pl;
}
```

Figure 13-10 The code for the enhanced ProductList class (part 2 of 2)
