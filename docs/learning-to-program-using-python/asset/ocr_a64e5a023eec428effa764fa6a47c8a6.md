```
(id INTEGER PRIMARY KEY,
name TEXT,
size TEXT,
price INTEGER)""")
```

```
for item in (
    (None, "Knife", "Small", 15),      #The end comma
    is required to separate tuple items
    (None, "Machete", "Medium", 35),
    (None, "Axe", "Large", 55),
    (None, "Hatchet", "Small", 25),
    (None, "Hammer", "Small", 25),
    (None, "Screwdriver", "Small", 10),
    (None, "Prybar", "Large", 60),
): cursor.execute("INSERT INTO Tools VALUES (?,
                ?, ?, ?)", item)
```

```
connection.commit()    #Write data to database
cursor.close() #Close database
```

The above code makes a simple, single-table database of a collection of hand tools. Notice the question marks used to insert items into the table. The question marks are used to prevent a SQL injection attack, where a SQL command is passed to the DB as a legitimate value. The DB program will process the command as a normal, legitimate command which could delete data, change data, or otherwise compromise your DB. The question marks act as a substitution value to prevent this from occurring.

You'll also note the ability to create a DB in memory. This is good for testing, when you don't want to take the time to write to disc or worry about directories. If you have enough memory, you can also create the DB completely in memory for your final product; however, if you lose power or otherwise have memory problems, you lose the complete DB. I only use a RAM DB when I'm testing the initial implementation to make sure I have the syntax and format correct. Once I verify it works the way I want, then I change it to create a disc-based DB.