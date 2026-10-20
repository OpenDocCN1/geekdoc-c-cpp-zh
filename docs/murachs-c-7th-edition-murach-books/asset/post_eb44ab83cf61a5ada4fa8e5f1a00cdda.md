
conventions when it generates the entity classes. In particular, it changes names so they use Pascal notation. So, for example, a column named CustomerID is changed to a property named CustomerId. If that’s not what you want, you can include the -UseDatabaseNames parameter.

If you don’t include the -Force parameter, you’ll get an error if you execute the Scaffold-DbContext command and the files that would be generated already exist. That way, you can’t unintentionally overwrite existing files. In some cases, though, you’ll need to regenerate the DB context and entity classes after making changes to the databases. To do that, you can use the -Force parameter to allow the overwriting of existing files.

When you use the Scaffold-DbContext command, you can code the flags for all parameters as shown in the first example. Alternatively, you can omit the flags for the two required parameters, -Connection and -Provider. If you do that, though, you need to be sure to code the value for the -Connection parameter first, followed by the value for the -Provider parameter.

## The Entity Data Model
for the MMABooks database

If the Scaffold-DbContext command runs without error, the Entity Data Model is created and displayed in the Solution Explorer as shown in figure 20-4. Here, the model is stored in the Models\DataLayer folder as specified by the command. This folder includes a DB context file named MMABooksContext.cs, as well as an entity class for each of the tables in the MMABooks database.

With EF Core 3.1 and earlier, the entity classes are given the same names as the database tables, which in this case are pluralized. By contrast, when you create your own objects, you typically use singular names. Unfortunately, these early versions of EF don’t provide a way to change the generated names from plural to singular. However, with EF Core 5.0, entity classes are given singular names, even if the names of the database tables are pluralized.

By the way, if you run the Scaffold-DbContext command and get a “Build failed” message, it’s because the source code for your application has syntax errors. Because of that, you’ll typically want to generate the Entity Data Model before you start coding an application.

## A Visual Studio project with an Entity Data Model

![](img/844f608d10a44654833ea5efc8a2e7a7_663_0.png)

## Description

- When the Scaffold-DbContext command completes, the generated files for the Entity Data Model are displayed in the Solution Explorer.
- Because Models\DataLayer was specified for the -OutputDir parameter, the generated files are stored in a folder with that name.
- Because MMABooksContext was specified for the -Context parameter, the DB context class is stored in a file named MMABooksContext.cs.

Figure 20-4  The Entity Data Model for the MMABooks database

## The code for the DB context class

To help you understand how a DB context class works, figure 20-5 shows the class that was generated for the MMABooks database. To start, you should notice that the code for this class is stored in a nested namespace. Specifically, it’s stored in a namespace named DataLayer (the name of the subfolder that contains the class) that’s nested within a namespace named Models (the name of the folder that contains the class). The Models folder in turn is nested within the namespace named CustomerMaintenance (the name of the project).

Next, you should notice that this class is declared as a partial class. Because of that, you can code additional partial classes that add to the generated class. Although you could code these changes in the generated partial class, this code would be lost if you regenerated the class. So, it’s a best practice to place this code in a separate partial class.

Finally, you should notice that this class inherits the DbContext class. When the DB context class is generated, EF includes code for the two methods of this class listed in the table at the top of this figure. You’ll learn more about these methods in just a minute.

The DB context class contains an empty constructor and a constructor that accepts a DbContextOptions object. This second constructor is used with dependency injection, which is beyond the scope of this book.

The constructors are followed by properties that define collections of DbSet<> objects for each of the entity classes. For example, the DbSet<Customers> object represents all of the Customer entities in the context. The DbSet<> class can be used to retrieve, add, update, and delete data.

The first method of the DB context class overrides the OnConfiguring() method of the DbContext class it inherits. This method receives a DbContextOptionsBuilder object that includes configuration information, such as the connection string for the database to be used. Then, an extension method of this object is used to configure the connection for the context. In this case, the UseSqlServer() method is used since the context will use a SQL Server database.

The second method of the DB context class overrides the OnModelCreating() method of the DbContext class. This method accepts a ModelBuilder object that provides the Fluent API that’s used to perform some of the configuration for the context and entity classes.

For example, the first three statements that configure the Customers entity use the IsUnicode() method to indicate that the Address, City, and Name properties can’t contain Unicode characters. Then, the next two statements use method chaining to call the IsUnicode() method followed by the IsFixedLength() method for the State and ZipCode properties. This works because each method returns an object that the next method in the chain can operate on.

The code for an entity can also include navigation properties that define relationships between entities in a way that makes sense in an object-oriented programming language. Navigation properties are convenient because they allow you to traverse related entities in code. EF Core creates a navigation property for each foreign key that’s defined for a table.

## Two methods of the DbContext class

| Method | Description |
|---|---|
| OnConfiguring(DbContextOptionsBuilder) | Called by the framework for each instance of the context that is created to configure the database used by this context. |
| OnModelCreating(ModelBuilder) | Called by the framework when the context is created to configure the context. |

## The DB context class generated by the Scaffold-DbContext command

```
using Microsoft.EntityFrameworkCore;

namespace CustomerMaintenance.Models.DataLayer
{
    public partial class MMABooksContext : DbContext
    {
        public MMABooksContext() {}

        public MMABooksContext(DbContextOptions<MMABooksContext> options)
            : base(options) {}

        public virtual DbSet<Customers> Customers { get; set; }
        public virtual DbSet<InvoiceLineItems> InvoiceLineItems { get; set; }
        public virtual DbSet<Invoices> Invoices { get; set; }
        public virtual DbSet<OrderOptions> OrderOptions { get; set; }
        public virtual DbSet<Products> Products { get; set; }
        public virtual DbSet<States> States { get; set; }

        protected override void OnConfiguring(
            DbContextOptionsBuilder optionsBuilder)
        {
            if (!optionsBuilder.IsConfigured)
            {
                optionsBuilder.UseSqlServer(
                    "Data Source=(LocalDB)\\MSSQLLocalDB;
                    AttachDBFilename=C:\\C#\\Database\\MMABooks.mdf;
                    Integrated Security=True");
            }
        }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Customers>(entity => {
                entity.Property(e => e.Address).IsUnicode(false);
                entity.Property(e => e.City).IsUnicode(false);
                entity.Property(e => e.Name).IsUnicode(false);
                entity.Property(e => e.State)
                    .IsUnicode(false)
                    .IsFixedLength();
                entity.Property(e => e.ZipCode)
                    .IsUnicode(false)
                    .IsFixedLength();
                entity.HasOne(d => d.StateNavigation)
                    .WithMany(p => p.Customers)
                    .HasForeignKey(d => d.State)
                    .OnDelete(DeleteBehavior.ClientSetNull)
                    .HasConstraintName("FK_Customers_States");
            });
        }
    }
}
```
