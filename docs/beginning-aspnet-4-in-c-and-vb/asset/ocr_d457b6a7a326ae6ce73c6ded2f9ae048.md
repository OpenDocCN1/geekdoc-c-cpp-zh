```
private void OnChangeBook(object sender, RoutedEventArgs e)
{
    Book theBook = this.DataContext as Book;
    if (theBook != null)
    {
        theBook.Title = "Professional C# 4 with .NET 4";
        theBook.Isbn = "978-0-470-50225-9";
    }
}
```

*code snippet BooksDemo/BookUC.xaml.cs*

To get change information to the user interface, the entity class must implement the interface INotifyPropertyChanged. The Book class is modified to implement this interface. This interface defines the PropertyChanged event, which also requires changing the implementation of the properties to fire the event:

```
using System.ComponentModel;
using System.Collections.Generic;

namespace Wrox.ProCSharp.WPF.Data
{
    public class Book : INotifyPropertyChanged
    {
        public Book(string title, string publisher, string isbn,
                    params string[] authors)
        {
            this.title = title;
            this.publisher = publisher;
            this.isbn = isbn;
            this.authors.AddRange(authors);
        }
        public Book()
            : this("unknown", "unknown", "unknown")
        {
        }

        public event PropertyChangedEventHandler PropertyChanged;

        private string title;
        public string Title
        {
            get
            {
                return title;
            }
            set
            {
                title = value;
                if (PropertyChanged != null)
                    PropertyChanged(this, new
                        PropertyChangedEventArgs("Title"));
            }
        }
        private string publisher;
        public string Publisher
        {
            get
            {
                return publisher;
            }
            set
            {

```