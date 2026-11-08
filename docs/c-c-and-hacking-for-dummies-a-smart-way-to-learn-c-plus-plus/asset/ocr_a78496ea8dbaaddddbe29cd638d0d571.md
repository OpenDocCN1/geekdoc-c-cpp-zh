future and we simply want a place for it to stay for the mean time. Hence, the core idea of a database.

# Keys

One of the vital elements of a relational database are keys. We now know that a table has several columns and each column has names. Each column has related properties as well. One of these properties that we can assert in a column is a key.

In a relational database, we always assign a primary key for each row. This special type of key is used to uniquely determine a specific row. This means that the value of that key must remain unique and must not have any duplicates within the table. If, and only if, there is another table which contains that key in our relation model; then, we may merge those two tables together.

When merging two tables, there will always be primary keys that have no duplicates. Upon merging, you will notice that there will be a new column in the table with these keys. These keys are now known as the Foreign keys. They serve as links to the primary keys of the second table, allowing you to conveniently link rows from two separated tables.

Aside from primary keys and foreign keys, we also have the natural keys. Natural keys are global. This means that you cannot change them since they are used all over the globe to identify a single entity. Published books, for instance, always have natural keys which we know as ISBN. Each published book has its own unique ISBN which you need to use as primary keys when handling relational database for books. This is different when handling databases with unnatural keys like emails, people, where you need to invent your own primary keys for each row.

Let us use a database for people and their contact numbers as an example. We cannot consider the name as the primary key. We cannot consider the person’s phone number as the primary key as well. This is because it is possible that there are two or more people in the globe that have the same contact number, first name, or even last name. Hence, we should create the primary key ourselves. This is where the identity column comes in.

The identity column serves as an auto-incrementing column that continues to generate unique keys as we add data in the table. The key combination does not matter since what we only need is a unique key for every identity in our database.