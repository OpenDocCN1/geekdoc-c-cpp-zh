
## The basic syntax of the join clause

```
join elementName in collectionName on keyName1 equals keyName2
```

### An example that joins data from two generic lists

### The Customer class

```
public class Customer
{
    public int CustomerID { get; set; }
    public string Name { get; set; }
}
```

### Code that gets the two data sources

```
List<Invoice> invoiceList = InvoiceDB.GetInvoices();
List<Customer> customerList = CustomerDB.GetCustomers();
```

### A query expression that joins data from the two data sources

```
var invoices = from invoice in invoiceList
    join customer in customerList
    on invoice.CustomerID equals customer.CustomerID
    where invoice.InvoiceTotal > 150
    orderby customer.Name, invoice.InvoiceTotal descending
    select new { customer.Name, invoice.InvoiceTotal };
```

### Code that executes the query

```
string invoiceDisplay = "Customer Name\t\tInvoice amount\n";
foreach (var invoice in invoices)
{
    invoiceDisplay += invoice.Name + "\t\t";
    invoiceDisplay += invoice.InvoiceTotal.ToString("c") + "\n";
}
MessageBox.Show(invoiceDisplay, "Joined Customer and Invoice Data");
```

![](img/844f608d10a44654833ea5efc8a2e7a7_617_0.png)

### Description

- The join clause lets you combine data from two or more data sources based on matching key values. The query results will include only those elements that meet the condition specified by the equals operator.
- You can extend the syntax shown above to join data from additional data sources.

## How to use extension methods and lambda expressions

Earlier in this chapter, I mentioned that the query operators provided by LINQ are implemented as methods and that you can call these methods directly rather than use the C# clauses for LINQ. In the topics that follow, you’ll learn how these methods work and how you use them to implement LINQ functionality.

### How extension methods work

Most of the methods that provide for LINQ functionality are implemented as extension methods. An extension method is similar to a regular method except that it’s defined outside the data type that it’s used with. The example in figure 18-8 shows how this works. Here, a method named FormattedPhoneNumber() is implemented as an extension method of the String class.

You should notice three things about the code that implements this method. First, it’s a static method that’s stored in a static class, which is a requirement for extension methods. Second, the data type of the first parameter of the method identifies the .NET class or structure that the method extends. In this case, the parameter is a string, so the method extends the String class. Third, the declaration for the first parameter is preceded by the this keyword.

Once you’ve defined an extension method, you can use it as shown in this figure. To start, you declare a variable with the same type as the first parameter of the method. In this case, a string variable is declared and assigned the digits of a phone number. Then, the extension method is executed as a method of that string. Notice that you don’t pass a value to the first parameter of the method. Instead, the value of the object on which the method is executed is assigned to this parameter. If any additional parameters are defined by the method, though, their values are passed to the method as shown here.

### An extension method that extends the String data type

### A class with an extension method that formats a phone number

```
public static class StringExtensions
{
	public static string FormattedPhoneNumber(this string phone, string separator)
	{
		return phone.Substring(0, 3) + separator
		       + phone.Substring(3, 3) + separator
		       + phone.Substring(6, 4);
	}
}
```

### Code that uses the extension method

```
string phoneNumber = "5595551212";
string formattedPhoneNumber = phoneNumber.FormattedPhoneNumber(".");
MessageBox.Show(formattedPhoneNumber + "\t", "Extension Method");
```

### The resulting dialog box

![](img/844f608d10a44654833ea5efc8a2e7a7_619_0.png)

- Extension methods provide for adding methods to a data type from outside the definition of that data type. Extension methods must be coded within a static class.
- The first parameter of an extension method identifies the data type it extends and must be preceded by the this keyword. You don’t pass a value to this parameter when you call the method. Instead, you call the method on an instance of the data type identified by the first parameter.

### How lambda expressions work

If you’ve read chapter 13, you already know how to use lambda expressions with delegates. In case you haven’t read that chapter, though, figure 18-9 summarizes the concepts for working with lambda expressions.

In short, a *lambda expression* is a function without a name that evaluates an expression and returns its value. As shown in this figure, the syntax of a lambda expression consists of a parameter list followed by the lambda operator and an expression. Note that if the lambda expression uses a single parameter, the parentheses can be omitted.

To use a lambda expression, you assign it to a *delegate* type, which specifies the signature of a method. The first example in this figure illustrates how this works. Here, the first statement defines a delegate type named compareDel that accepts a decimal value and returns a Boolean value. Then, the second statement declares a delegate of that type named invoiceOver150 and assigns a lambda expression to it. In this case, the lambda expression checks if a decimal parameter named total is greater than 150. If so, the expression will return a true value. Otherwise, it will return a false value.

In this example, the lambda expression is assigned to a variable. Then, in the code that executes the lambda expression, that variable is used to refer to the lambda expression and pass in the decimal value. When you use lambda expressions with LINQ, however, you code them inline as you’ll see next.

### The basic syntax of a lambda expression

```
(parameterList) => expression
```

### A lambda expression that tests a condition

### A statement that declares the delegate type at the class level

```
delegate bool compareDel(decimal total);
```

### A statement that defines the lambda expression and assigns it to a variable created from the delegate type

```
compareDel invoiceOver150 = total => total > 150;
```

### Code that executes the lambda expression

```
decimal invoiceTotal = 188.46m;
string invoiceMessage = "";
invoiceMessage += "Invoice Total: " + invoiceTotal.ToString("c") +
    "\n" + "Invoice over $150: " +
    invoiceOver150(invoiceTotal);
MessageBox.Show(invoiceMessage, "Invoice Test");
```

### The resulting dialog box

![](img/844f608d10a44654833ea5efc8a2e7a7_621_0.png)

### Description

- A lambda expression consists of an unnamed function that evaluates a single expression and returns its value.
- Lambda expressions are typically passed as arguments to methods that accept a delegate, which specifies the signature of a method. Many of the LINQ methods accept delegates as parameters as shown above. For more information on delegates, see chapter 13.

### How to code method-based queries

To code method-based queries, you use LINQ extension methods. For example, the table at the top of figure 18-10 lists the extension methods that are used to implement common C# clauses for LINQ. These extension methods define one or more parameters that accept lambda expressions. Like the invoiceOver150 variable you saw in the last figure, these parameters represent delegates that specify the signature of a method. For example, the second parameter of the Where() method is defined as a delegate that accepts a function with two parameters. The first parameter is the source element, and the second parameter is a Boolean expression.

The first example in this figure illustrates how this works. Here, the query uses four extension methods. This method-based query is equivalent to the query expression you saw in figure 18-6 that creates an anonymous type from the list of invoices. Each of the methods used by this query accepts a single lambda expression. For each lambda expression, the parameter list contains a single parameter that represents the source element, which is an invoice in this example. Then, the expression body for the lambda expression for the Where() method is a Boolean expression, the expression body for the OrderBy() and ThenByDescending() methods is an expression that specifies the field that’s used for sorting, and the expression body for the Select() method is an object that identifies the values to be returned by the query.

The second example in this figure is for a method-based query that joins data from the list of Invoice objects and the list of Customer objects. This is equivalent to the second query expression you saw in figure 18-7.

To join data from the two lists, the Join() method is executed on the list of Invoice objects. Then, four arguments are passed to this method. The first argument is the list of Customer objects that the list of Invoice objects will be joined with. The second and third arguments are lambda expressions that identify the fields of the Invoice and Customer objects that will be used to join the objects. In this case, an Invoice object will be joined with a Customer object if their CustomerID fields match. Finally, the fourth argument is a lambda expression that specifies the values to be included from the two objects. Note that for this to work, the lambda expression includes two parameters that identify the two objects.

The result of a join is an anonymous type that includes the fields specified by the fourth parameter. Then, any extension methods that follow are executed on this anonymous type. In this case, that includes the Where(), OrderBy(), and ThenByDescending() methods. Note that I’ve used a different parameter name in the lambda expressions for these methods to indicate that they refer to the anonymous type and not the Customer or Invoice objects.

Note also that this query doesn’t include a Select() method. That’s because the anonymous type that’s created by the join includes all of the fields needed by the methods that follow and all of the fields to be included in the results. If you needed to use additional fields in the query, though, and you didn’t want to include those fields in the results, you could include a Select() method that creates another anonymous type with just the fields you want. This is illustrated
