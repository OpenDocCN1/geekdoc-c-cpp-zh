# The ProductList class

| Indexer | Description |
| --- | --- |
| [index] | Provides access to the product at the specified position. |
| [code] | Provides access to the product with the specified code. |
| Property | Description |
| Count | An integer that indicates how many Product objects are in the list. |
| Method | Description |
| Add (product) | Adds the specified Product object to the list. |
| Add (code, description, price) | Creates a Product object with the specified code, description, and price values, and then adds the Product object to the list. |
| Remove (product) | Removes the specified Product object from the list. |
| Fill () | Fills the list with product data from a file. |
| Save () | Saves the products to a file. |
| Operator | Description |
| + | Adds a Product object to the list. |
| - | Removes a Product object from the list. |
| Delegate | Description |
| ChangeHandler | Can be used to register the method that's used to handle the Changed event. |
| Event | Description |
| Changed | Raised whenever a Product object is added to, updated in, or removed from the list. |

Figure 13-2 The specifications for the enhanced ProductList class