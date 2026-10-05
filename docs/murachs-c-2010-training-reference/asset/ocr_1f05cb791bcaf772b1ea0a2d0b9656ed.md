# How to work with indexers

In the topics that follow, you'll learn two skills for working with indexers. First, you'll learn how to code an indexer. Then, you'll learn how to throw an argument exception if the argument's passed to the indexer isn't valid.

# How to create an indexer

As figure 13-3 shows, an indexer is a special type of property that lets you create classes that represent collections of objects. An indexer lets others use the class access for a specific item in the collection by specifying an index value.

The first example in this figure shows an indexer for the ProductList class. Notice that this class starts by declaring a private List<> field named products. This list will be used to store products within a ProductList object. Then, an indexer with the type Product is declared. Notice that this index is not given a name. Instead, it uses the keyword to refer to the current object. The keyword is followed by a parameter that identifies the index used by the index. Unlike most parameters, which are coded in parentheses, the parameter for an indexer is coded with brackets.

Like any other property, an indexer can provide get and setters. For example, the get accessor in the first example uses an integer index to return a Product object from the products list based on its position in the list. Conversely, the setter allows you to assign a Product object to the products list at the specified integer index.

The second example in this figure shows another possible indexer for the ProductList class. This indexer varies from the first one in two ways. First, it doesn't include a setter accessor, so it provides read-only access to the products. Second, it uses a string index that provides for accessing the products by product code. To do that, this get accessor uses a foreach loop to search the products list, and returns the first product whose Code matches the index value. If no match is found, null is returned.

The third example in this figure shows how you can use these indexers. The first two statements create a new ProductList object and add a product to it using the Add method. Then, the next two statements use the two indexers in this figure to retrieve products from the list by index and by product code. Finally, the last statement in this group uses the setter accessor to add a new product to the list at the index specified by the variable i.