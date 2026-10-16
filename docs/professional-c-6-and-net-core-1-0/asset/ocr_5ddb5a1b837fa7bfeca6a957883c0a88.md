```
public class Book
{
    public Book()
    {
        Chapters = new List<Book>();
    }

    public int BookId { get; set; }
    public string Isbn { get; set; }
    public string Title { get; set; }
    public List<Chapter> Chapters { get; }
}
```

The Chapter class defines simple properties and a many-to-one relation to the Book type (code file BooksODataService/Models/Book.cs):

```
public class Chapter
{
    public int ChapterId { get; set; }
    public int BookId { get; set; }
    public Book Book { get; set; }
    public string Title { get; set; }
    public int Number { get; set; }
    public string Intro { get; set; }
}
```

The BooksContext class defines the Books and Chapters properties as well as the definition of the SQL database relations (code file BooksODataService/Models/BooksContext.cs):

```
public class BooksContext: DbContext
{
    public DbSet<Book> Books { get; set; }
    public DbSet<Chapter> Chapters { get; set; }

    protected override void OnModelCreating(ModelBuilder modelBuilder)
    {
        base.OnModelCreating(modelBuilder);
        EntityTypeBuilder<Book> bookBuilder = modelBuilder.Entity<Book>();
        bookBuilder.HasMany(b => b.Chapters)
            .WithOne(c => c.Book)
            .HasForeignKey(c => c.BookId);
        bookBuilder.Property<string>(b => b.Title)
            .HasMaxLength(120)
            .IsRequired();
        bookBuilder.Property<string>(b => b.Isbn)
            .HasMaxLength(20)
            .IsRequired(false);

        EntityTypeBuilder<Chapter> chapterBuilder = modelBuilder.Entity<Chapter>();
        chapterBuilder.Property<string>(c => c.Title)
            .HasMaxLength(120);
    }
}
```

# Creating a Service

With ASP.NET Core 5, you can easily add OData Services. You don’t need to make many changes to a controller. Of course, you need to add