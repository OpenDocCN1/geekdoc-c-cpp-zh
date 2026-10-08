**4. Create Author and Category entities, respectively.**

The author and category of a book might both be considered properties of a book, and in fact, you could define them that way. However, in this application, define both the Category and Author as entities instead (see Figure 19-4). That way, you can alter the author names and categories later without changing the author and category for each book in the collection.

![](bbox=[0.13, 0.25, 0.2, 0.31])

If the three entities appear on top of one another on the graph paper-looking pane, move them by clicking and dragging each entity so you can see them better.

![](bbox=[0.25, 0.33, 0.85, 0.67])

**Figure 19-4:** Create the Author and Category entities.

**5. Select the Book entity and then click the + button at the bottom of the Property pane to add an attribute to the Book entity.**

There are three kinds of properties: attributes, fetched properties, and relationships, which all appear in the pop-up menu that opens when you click the + button in the Property pane. For now, you need only concern yourself with the attributes property type.

**6. Name the new attribute *title* and make it a non-optional String type.**