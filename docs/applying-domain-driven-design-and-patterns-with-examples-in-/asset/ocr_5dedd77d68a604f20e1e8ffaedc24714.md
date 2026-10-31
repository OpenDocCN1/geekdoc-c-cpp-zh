deal with this would be to create a "superset" client-side Customer Domain Model object with properties for all the different fields that were returned from all the companies called.

Next, we want the user of the Rich Client application to be able to look at the orders belonging to a particular customer. The unique ID of each customer was of course included in the XML document returned by the first Web Service, so we know the ID of the customer in which we're interested.

What I have to do is to implement a Web Service that takes the ID of a customer and returns the orders for that customer. Again, I begin by creating a GetOrdersByCustomerID() Service Layer method that accepts the ID of a customer and returns the Domain Model Order objects belonging to the customer.

I'll then proceed by adding a GetOrdersByCustomerID() Web Service that takes a customer ID, passes it along to the Service Layer method, and finally serializes the returned order objects into an XML document that can be returned by the Web Service.

However, in this case, some extra attention has to be paid to the XML serialization. We want the XML document to include the total value for each order, but the Order Domain Model object doesn't contain any TotalValue property because the total value of an order is not stored in any field in the database.

Rather, the total value is calculated whenever it is needed by adding the values of the order lines together. The value of each order line, in its turn, is calculated by multiplying the price that the purchased product had when it was bought by the number of items bought.

Because the order lines aren't included in the XML document sent to the client, the client application can't calculate the total values for the orders, which means that the calculation has to be done on the server and the result has to be included in the XML document.

The methods for calculating the value of an order line and the total value for an order are good examples of the type of method that many people would prefer to put on the OrderLine and Order Domain Model objects but that I prefer to put in the Service Layer.

# Service Layer Design

This may be a good time to mention that I usually organize my Service Layer around the same entities that are used in the Domain Model, rather than by task, which is otherwise also popular. This means that if I have an Employee object in the Domain Model Layer, I'll have an EmployeeServices class in the Service Layer.

For services that don't need any transaction control, I also usually implement the Service Layer methods as static methods so that they can be called without instantiating any object from the Service Layer classes.

In the case at hand, I would thus place a static GetValue() method on the OrderLineServices Service Layer class and a static GetTotalValue() method on the OrderServices class. These methods will accept the objects they should work with as parameters. This means I won't be calling a method on the Order object itself in the following fashion:

```
myOrder.GetTotalValue();
```