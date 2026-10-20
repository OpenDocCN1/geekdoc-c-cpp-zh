
## The code for the ProductList class

```
public class ProductList
{
    private List<Product> products;

    public delegate void ChangeHandler(ProductList products);
    public event ChangeHandler Changed;

    public ProductList()
    {
        products = new List<Product>();
    }

    public int Count => products.Count;

    public Product this[int i]
    {
        get
        {
            if (i < 0)
            {
                throw new ArgumentOutOfRangeException(i.ToString());
            }
            else if (i >= products.Count)
            {
                throw new ArgumentOutOfRangeException(i.ToString());
            }
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

## Section 3 Object-oriented programming

The Fill() method of the ProductList class, shown on page 2 of this listing, calls the GetProducts() method of the ProductDB class to get products from a file. Similarly, the Save() method calls the SaveProducts() method of this class to save the products to a file.

The ProductList class also provides two overloads for the Add() method: one that accepts a Product object and one that accepts a code, description, and price. It also includes a Remove() method that removes the specified Product object. As you can see, all three of these methods raise the Changed event.

Finally, this class provides an overloaded + operator and an overloaded - operator. The overloaded + operator calls the first Add() method to add the specified object to the product list and then returns the updated product list. Similarly, the - operator calls the Remove() method to remove the specified product from the product list and then returns the updated product list.

## The code for the Product Maintenance form

Figure 13-13 shows the code for the enhanced version of the Product Maintenance form. Because most of this code is the same as in chapter 12, I’ve highlighted the key differences here.

First, the products variable that’s used by the class to store Product objects is a ProductList object, not a List<> object. As a result, this version of the application can use the features of the ProductList class, such as the indexer, the Fill() and Save() methods, the overloaded + and - operators, and the Changed event.

In the Load event handler for the form, the ChangeHandler delegate is used to wire the HandleChange() method (which appears at the end of the listing) to the Changed event of the products object. As you have seen in the ProductList class, this event is raised any time a product is added to, removed from, or changed in the product list. Then, the HandleChange() method calls the Save() method of the products object to save the new list, and it calls the FillProductListBox() method to refresh the list box.

After it wires the Changed event, the Load event handler calls the Fill() method of the products object to fill the product list. Then, it calls the FillProductListBox() method to fill the list box. Notice that this method uses a for loop to retrieve each product in the product list by its index.

The Click event handler for the Add button calls the GetNewProduct() method of the New Product form to get a new product. Then, if the Product object that’s returned by this method isn’t null, the += operator is used to add the product to the product list.

The Click event handler for the Delete button uses an indexer of the ProductList class to retrieve the selected product from the product list. Then, assuming the user confirms that the product should be deleted, it uses the -= operator to remove the product from the list.

```
private ProductList products = new ProductList();

private void frmProductMain_Load(object sender, EventArgs e)
{
    products.Changed += new ProductList.ChangeHandler(HandleChange);
    products.Fill();
    FillProductListBox();
}

private void FillProductListBox()
{
    Product p;
    lstProducts.Items.Clear();
    for (int i = 0; i < products.Count; i++)
    {
        p = products[i];
        lstProducts.Items.Add(p.GetDisplayText("\t"));
    }
}

private void btnAdd_Click(object sender, EventArgs e)
{
    frmNewProduct newForm = new frmNewProduct();
    Product product = newForm.GetNewProduct();
    if (product != null)
    {
        products += product;
    }
}

private void btnDelete_Click(object sender, EventArgs e)
{
    int i = lstProducts.SelectedIndex;
    if (i != -1)
    {
        Product product = products[i];
        string message = "Are you sure you want to delete "
            + product.Description + "?";
        DialogResult button = MessageBox.Show(message, "Confirm Delete",
            MessageBoxButtons.YesNo);
        if (button == DialogResult.Yes)
        {
            products -= product;
        }
    }
}

private void btnExit_Click(object sender, EventArgs e)
{
    this.Close();
}

private void HandleChange(ProductList products)
{
    products.Save();
    FillProductListBox();
}
```

## Perspective

In this chapter, you’ve learned about a variety of features that you can include in the classes you create. You should keep in mind, however, that not all classes require these features. In fact, most classes require just the features you learned about in chapter 12. Nevertheless, it’s important that you know about the features presented in this chapter so you can use them when that’s appropriate.

Now that you’ve read this chapter, you should begin to appreciate the power and complexity of C# classes. Still, there’s much more to learn about coding C# classes than what’s presented here. In the next chapter, then, you’ll learn about one of the most important and potentially confusing aspects of object-oriented programming in C#: inheritance.

## Terms

- indexer
- indexer overloading
- expression-bodied indexer
- delegate
- signature of a delegate
- event
- anonymous method
- overload an operator
- operator overloading
- expression-bodied operator
- hash code

## Exercise 13-1 Create a Customer Maintenance application that uses classes

In this exercise, you’ll create a Customer Maintenance application that uses classes with the features presented in this chapter. To make this application easier to develop, we’ll give you the starting forms and classes.

### Open the project and add validation code to the Customer class

1. Open the application in the C:\C#\Chapter 13\CustomerMaintenance directory.
2. Open the Customer class and note how the constructor for this class sets the properties to the appropriate parameters. Then, add code to the set accessors for the FirstName, LastName, and Email properties that throws an exception if the value is longer than 30 characters.
3. Test the class by trying to add a new customer with an email address that’s longer than 30 characters. When you do, an exception should be thrown. Then, end the application.
4. Set the MaxLength properties of the First Name, Last Name, and Email text boxes to 30. Then, run the application again and try to add a new customer with an email address that’s longer than 30 characters. This shows one way to avoid the exceptions, but your classes should still throw them in case they are used by other applications that don’t avoid them.

### Add a CustomerList class

5. Add a class named CustomerList to the project, and declare a private variable that can store a list of Customer objects.

6. Add the following members to the CustomerList class, coding Count as an expression-bodied property and Fill() and Save() as expression-bodied methods.

| Constructor | Description |
| --- | --- |
| () | Creates a new list of Customer objects. |

| Indexer | Description |
| --- | --- |
| [index] | Provides access to the Customer at the specified position. |

| Property | Description |
| --- | --- |
| Count | An integer that indicates how many Customer objects are in the list. |

| Method | Description |
| --- | --- |
| Add(customer) | Adds the specified Customer object to the list. |
| Remove(customer) | Removes the specified Customer object from the list. |
| Fill() | Fills the list with customer data from a file using the GetCustomers() method of the CustomerDB class. |
| Save() | Saves the customers to a file using the SaveCustomers() method of the CustomerDB class. |

7. Modify the Customer Maintenance form to use this class. To do that, you’ll need to use the Fill() and Save() methods of the CustomerList object instead of the methods of the CustomerDB class. In addition, you’ll need to use a for loop instead of a foreach loop when you fill the list box.

8. Run the application and test it to be sure it works properly.

## Exercise 13-2 Use overloaded operators

In this exercise, you’ll enhance the Customer Maintenance application from exercise 13-1 so it uses overloaded operators to add and remove customers from the customer list.

1. If it isn’t open already, open the application in the C:\C#\Chapter 13\CustomerMaintenance directory.
2. Add overloaded + and - operators to the CustomerList class that add and remove a customer from the customer list.
3. Modify the Customer Maintenance form to use these operators instead of the Add() and Remove() methods.
4. Run and test the application to make sure it works correctly.
