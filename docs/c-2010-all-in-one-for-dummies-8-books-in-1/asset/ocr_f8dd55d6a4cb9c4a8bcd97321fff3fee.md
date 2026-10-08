# Using the System.DataNamespace

Lines 5, 6, and 7 perform the magic: Open the connection, contact the data-base. Fill the dataset using this adapter, and then close the database. It's all straightforward in this simple example. More complex examples make for more complex code.

After running this code, you would have the Parts table in a DataSet container as you did in the visual tools in the earlier section, "How the Data Fits into the Framework". To access the information, you can set the value of a text box to the value of a cell in the DataSet container, like this:

```
TextBox1.Text = myData.Tables[0].Rows[0]["part_name"]
```

To change the next record, you would need to write code that changes the Rows[0] to Rows[1] in the next example. As you can see, it would be a fair amount of code.

That's why few people use the basic data to get the databases. Either you use the visual tools or use a data broker of some sort.

# Using the Entity Framework

I don't want to get into this programming philosophy here, but object models (which I discuss in this book) and databases don't just go together. They're two different ways of thinking of the same information.

The problem mostly lies in inheritance, which I discuss in Book II. If you have a class called ScheduledEvent, which has certain properties, and a bunch of classes that inherit from it, like Courses, Conferences, and Parties, then just isn't a good way to show this in a relational type of database.

If you make a table for ScheduledEvents with all possible types of properties, and make a Type property so you can use the Courses from the Parties, and then you will have a lot of empty cells. If you make a table for the properties that are in ScheduledEvents, and then separate tables for Courses and Parties, you make the database remarkably complex.

To address this problem, Microsoft created the Entity Framework. It's the latest edition of a product that Microsoft and everyone else has tried to create since the popularity of relational databases and object-oriented programming made object role models necessary.

Object Role Models try and take the whole shootin' match turn on its head. The goal is to design the database first (which I recommend anyway), and then make an object model to work with it automatically. Then, keep it up to date.