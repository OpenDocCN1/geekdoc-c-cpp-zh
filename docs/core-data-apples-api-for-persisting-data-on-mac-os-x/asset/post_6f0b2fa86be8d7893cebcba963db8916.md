
![](img/ffa5f756dbdb501d7886468ffb761ad4_110_0.png)

Figure 6.4: Impacts of deleting a recipe

Author entity, Ingredient entity, and UnitOfMeasure entity, as shown in Figure 6.4.

It is obvious that we need to touch the RecipeIngredient entity, but why do we need to access all the others? This is because of the relationships between the entities. For each relationship, we need to validate the relationship after the delete and confirm that there are no dangling references. If these objects are not currently in memory, then the NSManagedObjectContext must retrieve them from the disk to accomplish all of this.

Therefore, when we are doing deletes, especially large deletes, it can be a performance improvement to fetch all the relationships prior to the delete.

### Faulting and Disk Access

Firing a fault does not always mean that the data is going to be read from disk. Depending on how we have requested the data in the first place or what happened earlier in the NSManagedObject object’s life span, it is quite possible that the data will be loaded from cache instead.

Likewise, faulting an NSManagedObject does not guarantee that it will be written back out to disk nor does it guarantee that it will be removed from the cache. If the object has no changes, then there is nothing to write to disk, and it is quite possible that it will remain in the cache for an unknown period of time.

Easily one of the best ways to check to see whether the firing of a fault is in fact causing disk access is to monitor our application with Instruments. By using the Core Data template, we can use the “cache miss” instrument to check for disk hits. If we are getting far more calls to the disk than expected, then we need to consider refactoring the code.

### 6.5 Access Patterns

Improving performance within Core Data is not necessarily only about the repository and order of loading the data. There are a number of things that we can do within the user interface to help performance as well.

### Searching

Searching the repository can be absolute murder on performance. Whether we are searching at the request of the user or we are performing a search in the background, we need to be very careful to avoid impacting the performance of our application.

### Order Is Important

Just like any conditional, the order of the logic is important. Simple equality is faster than inclusions such as in, contains, and so on. When building the predicate, try to order the logic from left to right, simple to complex. This will allow Core Data to fail quickly and improve the search performance.

### Unicode and Regular Expressions

Unicode is very expensive to work with when we are searching. As suggested earlier in Section 6.2, Search Only Properties, on page 102, try to avoid searching against Unicode directly. It is cheaper to keep a derived value that strips off the Unicode than it is to do frequent searches against the Unicode text.

Likewise, regular expressions are expensive. If a situation calls for one, try to put it at the far right end of the NSPredicate, as discussed in Section 6.5, *Order Is Important*, on the previous page.

### Limit Queries Across Relationships

Searching across objects that are joined by a relationship can be very expensive for searching. Although it is impressive to search against person.address.postalCode.city, it may not be the most efficient way to solve the problem. Consider reversing the query or breaking it down into several smaller queries to reduce the complexity of the underlying SQL. When we are working with a SQLite back end, all of our NSPredicate calls turn into SQL before hitting the database. The less complex that SQL is, the faster it will run. It may very well be faster to get an NSArray of all the Address objects within a specific city and then perform the rest of the query against that NSArray than it would be to traverse three relationships in one call.

### Information Overload

A busy user interface is more than just a poor user experience; it also impacts the performance of the application. When we display a large amount of data on the screen, we must keep that information in memory, which in turn means we must load a large amount of data from disk all in one go. It is far better to break an application user interface up into consumable chunks of information than it is to try to display every last bit on the screen at once.

The careful use of tabs, sheets, and panels can improve the feel of a user interface, and that will in turn improve the performance. By splitting the user interface into smaller pieces, we have finer-grained control over what data gets loaded when, and we can reduce our disk access to manageable chunks.

Keep it simple.

## Chapter 7: Spotlight, Quick Look, and Core Data

Developing for Mac OS X is about functionality meeting quality. When our applications have either without the other, we leave our users wanting more. They may not be able to define it, but “something” will be missing. Spotlight and Quick Look integration are two of those things that users don’t look for when trying a new application but are pleasantly surprised by them when they stumble upon them. Surprisingly, not a lot of developers handle this integration. Perhaps it is because Spotlight does not get along with Core Data very well. Perhaps the feature is too new. But one thing is for certain—integrating with Spotlight is the right move going forward. Spotlight is here to stay, and users will be using it more often and in more creative ways.

Unfortunately, for technical reasons, Spotlight and Core Data are at odds with each other. Spotlight works on the metadata of individual files, and Core Data stores everything in a single file. Because Spotlight is designed to work with the metadata of a file to discover things about the file, it will not work very well with a single file design such as Core Data. When Tiger was first released, there were a number of applications (such as Entourage) that, because of their single file design, did not play nicely with Spotlight. In fact, Apple rearchitected Mail for that reason.

The incompatibility between Spotlight and Core Data is corrected in Snow Leopard but unfortunately it’s Snow Leopard only and not backward compatible with plain old vanilla Leopard. How? It’s in a manner that is very similar to the solution described in this chapter.

### Should I Just Use Separate Files?

Throughout this book, the application we are designing uses a single Core Data file. This is done for the sake of clarity and focus on Core Data. Depending on the application that is being designed, it is highly likely that it will be document based, and therefore it would be appropriate to have one Core Data repository per document. In that situation, Spotlight and Quick Look can be a lot easier to integrate.

However, for applications that are not document based, then it is preferable to use a single Core Data repository as opposed to individual files. Although individual files will make Spotlight easier to work with, it would be the tail wagging the dog. The main focus of object persistence (in other words, data files) is to quickly and easily access the data in a logical and reproducible manner. Core Data solves all those problems quite neatly with the unfortunately minor side effect of not being fully compatible with Spotlight.

In this chapter, we will integrate Spotlight into our recipes application. Once we are done, our users will be able to search for *Pot Roast* and find it in our application. In addition, when they select that search result, our application will not only open but open to Pot Roast. While we are solving the Spotlight issue, we are also going to take a look at Quick Look. Although on the surface these two technologies appear to be completely different, they are handled in a very similar fashion by Mac OS X and the Finder. And although it is not 100 percent appropriate for our sample application (since we have only a single data file and that data file is hidden away in the Library/Application Support directory), it is very useful to understand how Quick Look works for document-based Core Data applications because it makes them easier to find in Finder, Spotlight, Time Machine, Mail, and many other applications. Lastly, Quick Look and Spotlight integrate rather well together. If our users activate Quick Look on a Spotlight result, we want them to see information about the recipe, not a picture of a generic file.
