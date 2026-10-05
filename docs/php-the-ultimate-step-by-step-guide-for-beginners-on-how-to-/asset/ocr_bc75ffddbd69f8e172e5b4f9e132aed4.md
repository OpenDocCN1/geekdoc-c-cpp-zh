Rather than utilizing the WHERE pivotal word, LEFT JOIN ON can be utilized to perform left or external join. A left join essentially permits you to inquiry two tables that are connected together by a relationship, yet permits one of the tables to return lines regardless of the possibility that isn't a coordinating line in the other table. Utilizing the book shop tables as an illustration, you may need to make an inquiry that profits clients and their buys, additionally records clients who have yet to buy anything.

Using the punctuation:

```
SELECT fields FROM left_table JOIN right_table ON left_table.field_id =ight_
table.field_id; your objective could be refined like this:

SELECT * FROM clients LEFT JOIN buys users.user_id = =
purchases.user_id;
```

If you'd like to attempt this inquiry, you'll have to make the clients table and include some information:

```
Make TABLE clients (
user_id int(110) NOT NULL auto_increment,
first_name varchar(100) default NULL,
last_name varchar(100) default NULL,
username varchar(45) default NULL,
secret key varchar(32) default NULL,
Essential KEY (user_id)
);
Embed INTO clients VALUES
(1,'Michele','Davis','mdavis',NULL),(2,'Jon','Phillips','jphillips',NULL);
```

While doing an ordinary database query that connections two tables, if both tables don't incorporate the key qualities for the field being joined, nothing is returned for the passage.

# Using Database Functions