limitation would mean that “Jones” might follow “Smith,” which would in turn be followed by “Baker.” In other words, there is no particular order to the data stored in this file.

An unsorted Rolodex like this would be very difficult to use. You’d have to search each and every card looking for a particular person, a painful and time-consuming process. Of course, this isn’t how you use address card files. When you add a card to the file, you insert it into the Rolodex at your location where it logically belongs. Most often, this means inserting the card in alphabetical order, by last name, into the Rolodex.

Records are added to Access tables as described in the fixed card file example earlier. New records are always added to the end of the table, rather than in the middle of the table where they may logically belong. However, in an order-entry system, you’d probably want new records inserted next to other records on the same customer. Unfortunately, this isn’t how Access tables work. The *natural order* of a table is the order in which records were added to the table. This order is sometimes referred to as *entry order* or *physical order* to emphasize that the records in the table appear in the order in which they were added to the table.

Using tables in natural order is not necessarily a bad thing. Natural order makes perfect sense if the data is rarely searched or if the table is very small. Also, there are situations where the data being added to the table is highly ordered to start with. If the table is used to gather sequential data (like readings from an electric meter) and the data will be used in the same sequential order, there is no need to impose an index on the data.

But for situations where natural order doesn’t suffice, Access provides *indexing* to help you find and sort records faster. You specify a *logical* order for the records in a table by creating an *index* on that table. Access uses the index to maintain one or more internal sort orders for the data in the table. For example, you may choose to index the LastName field that will frequently be included in queries and sorting routines.

Access uses indexes in a table as you use an index in a book: to find data. Access looks up the data’s location in the index. Most often, your tables will include one or more *simple indexes*. A simple index is one that involves a single field in the table. Simple indexes may arrange the table’s records in ascending or descending order. Simple indexes are created by setting the field’s Indexed property to one of the following values:

+   - Yes (Duplicates OK)
+   - Yes (No Duplicates)

By default, Access fields are not indexed, but it’s hard to imagine a table that doesn’t require some kind of index. The next section discusses why indexing is important to use in Access tables.

# The importance of indexes

Microsoft’s data indicates that more than half of all tables in Access databases contain no indexes. This number doesn’t include the tables that are improperly indexed—it includes