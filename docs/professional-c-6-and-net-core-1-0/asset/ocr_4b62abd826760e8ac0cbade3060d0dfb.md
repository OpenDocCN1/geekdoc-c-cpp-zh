```
public ICommand SaveBookCommand { get; }

private void LoadBook(object sender, BookInfoEvent bookInfo)
{
	if (bookInfo.BookId == 0)
	{
		Book = new Book();
	}
	else
	{
		Book = _booksService.GetBook(bookInfo.BookId);
	}
}

public void Dispose()
{
	EventAggregator<BookInfoEvent>.Instance.Event -= LoadBook;
}
// etc.
```

The event is published when a book is selected in the ListBox, and thus the SelectedBook property calls the set accessor. Here, the EventAggregator can be accessed similar to subscription using the static Instance property, now by invoking the Publish method, which passes a BookInfoEvent object (code file ViewModels/BooksViewModel.cs):

```
private Book _selectedBook;
public Book SelectedBook
{
	get { return _selectedBook; }
	set
	{
		if (SetProperty(ref _selectedBook, value))
		{
			EventAggregator<BookInfoEvent>.Instance.Publish(
				this, new BookInfoEvent { BookId = _selectedBook.BookId });
		}
	}
}
```

With the messaging mechanism in place, you can start the application, select books, and add them as shown in Figure 31.11.

![](bbox=[0.1, 0.82, 0.9, 0.95])

# IoC Container