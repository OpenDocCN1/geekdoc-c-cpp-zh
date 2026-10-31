# # A First Sketch

To make it a bit more concrete, let's use a list of problems/features to discuss how some common design problems of an ordering application could be solved.

I know, I know. The answer to how I would deal with the feature list with my current favorite style of a Domain Model depends on many factors. As I said before, talking about a "default architecture" is strange because the architecture must first and foremost depend on the problem at hand.

However, I still want to discuss a possible solution here. It will be very much a sketched summary, with details following in later chapters. What I will be discussing here will be kind of a first rough attempt, and I will leave it like that, letting the design evolve in later chapters.

# ## Problems/Features for Domain Model Example

I will reuse this list of requirements in later chapters for discussing certain concepts. Let's dive in and examine the details for each problem/feature in random order.

+   1. List customers by applying a flexible and complex filter.
+   
+      The customer support staff needs to be able to search for customers in a very flexible manner. They need to use wildcards on numerous fields such as name, location, street address, reference person, and so on. They also need to be able to search for customers with orders of a certain kind, with orders of a certain size, with orders for certain products, and so on. What we’re talking about here is a full-fledged search utility. The result is a list of customers, each with a customer number, customer name, and location.
+   
+   2. List the orders when looking at a specific customer.
+   
+      The total value for each order should be visible in the list, as should the status of the order, type of order, order date, and name of reference person.
+   
+   3. An order can have many different lines.
+   
+      An order can have many order lines, where each line describes a product and the number of that product that has been ordered.
+   
+   4. Concurrency conflict detection is important.
+   
+      It's alright to use optimistic concurrency control. That is, it's accepted that when a user is notified after he or she has done some work and tries to save, there will be a conflict with a previous save. Only conflicts that lead to real inconsistencies should be considered conflicts. So the solution needs to decide on the versioning unit for customers and for orders. (This will slightly affect some of the other features.)