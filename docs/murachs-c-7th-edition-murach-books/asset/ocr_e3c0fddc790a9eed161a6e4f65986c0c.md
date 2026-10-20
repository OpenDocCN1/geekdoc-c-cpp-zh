# The code for the DB context class

To help you understand how a DB context class works, figure 20-5 shows the class that was generated for the MMABooks database. To start, you should notice that the code for this class is stored in a nested namespace. Specifically, it’s stored in a namespace named DataLayer (the name of the subfolder that contains the class) that’s nested within a namespace named Models (the name of the folder that contains the class). The Models folder in turn is nested within the namespace named CustomerMaintenance (the name of the project).

Next, you should notice that this class is declared as a partial class. Because of that, you can code additional partial classes that add to the generated class. Although you could code these changes in the generated partial class, this code would be lost if you regenerated the class. So, it’s a best practice to place this code in a separate partial class.

Finally, you should notice that this class inherits the DbContext class. When the DB context class is generated, EF includes code for the two methods of this class listed in the table at the top of this figure. You’ll learn more about these methods in just a minute.

The DB context class contains an empty constructor and a constructor that accepts a DbContextOptions object. This second constructor is used with dependency injection, which is beyond the scope of this book.

The constructors are followed by properties that define collections of DbSet<> objects for each of the entity classes. For example, the DbSet<Customers> object represents all of the Customer entities in the context. The DbSet<> class can be used to retrieve, add, update, and delete data.

The first method of the DB context class overrides the OnConfiguring() method of the DbContext class it inherits. This method receives a DbContextOptionsBuilder object that includes configuration information, such as the connection string for the database to be used. Then, an extension method of this object is used to configure the connection for the context. In this case, the UseSqlServer() method is used since the context will use a SQL Server database.

The second method of the DB context class overrides the OnModelCreating() method of the DbContext class. This method accepts a ModelBuilder object that provides the Fluent API that’s used to perform some of the configuration for the context and entity classes.

For example, the first three statements that configure the Customers entity use the IsUnicode() method to indicate that the Address, City, and Name properties can’t contain Unicode characters. Then, the next two statements use method chaining to call the IsUnicode() method followed by the IsFixedLength() method for the State and ZipCode properties. This works because each method returns an object that the next method in the chain can operate on.

The code for an entity can also include navigation properties that define relationships between entities in a way that makes sense in an object-oriented programming language. Navigation properties are convenient because they allow you to traverse related entities in code. EF Core creates a navigation property for each foreign key that’s defined for a table.