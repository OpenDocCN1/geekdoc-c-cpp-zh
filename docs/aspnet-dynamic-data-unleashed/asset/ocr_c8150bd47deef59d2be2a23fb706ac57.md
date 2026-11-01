# Validation Rule Design

To find a reasonable compromise between code reuse, complexity, and performance, without having to do a lot of refactoring later, try the following rules of thumb when designing validation logic in your application:

+   - Implement persistence validation rules with data annotations
+   - Make state properties of entities read-only
+   - Implement state transitions and validation in business rule methods
+   - Implement state-specific persistence validation in separate validation methods

# Implement Persistence Validation Rules with Data Annotations

The validation framework discussed in Chapter 8 offers a great way to implement persistence validation rules by applying pre-built validation attributes or writing custom validation methods for individual properties or entire entities. You can quickly apply the RequiredAttribute to the shipping address properties of the Order entity to ensure that the order is valid before saving it to the database.

# Make State Properties of Entities Read-Only

You do not want the users of your application (neither the customers nor the employees) to edit the OrderStatus property directly, even if they initiate the state transition. Customers will submit orders by clicking a Submit button on a check-out page, and a background process handling credit card payments will mark the orders as paid. The best way to ensure that state properties of an entity cannot be changed through the user interface of the application is to make them read-only.

With Entity Framework, you can use the Entity Designer to make the setter of the OrderStatus property internal, as shown in Figure 9.7.