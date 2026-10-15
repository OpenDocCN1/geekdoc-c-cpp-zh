In Listing 16.2, you saw the following code that creates an instance of the RemoveBookCommand object:

```
RemoveBookCommand = new RelayCommand(
    () => Messenger.Default.Send<RemoveBookMessage>(
        new RemoveBookMessage(this));
```

In this code I’m saying that every time the RemoveBookCommand is executed (regardless of how or why it is executed) that the current view model (Book) will send a message to all subscribers indicating that a book has been marked for removal.

Why not just make sure that each instance of the Book view model has a reference to the MainView model? This way the book could just remove itself directly from the list. The problem with this pattern is that it violates the “don’t look up” principal of MVVM development, and it means that anytime we want any other view model to respond to the deletion of a book, we have to put that code in the Book view model rather than in the appropriate view models.

# Don’t Look Up

> Jesse Liberty has a very popular quote about MVVM development that says, quite simply, “don’t look up.” Keep this in mind when building your view models and it will help guide you to a better MVVM architecture. In short, never reference anything from a view model that is “higher” than the view model. That means your view model shouldn’t be able to reference parent view models directly, nor should it ever have a direct reference to the view page (XAML) associated with that view. In our case, the Book view model should never have a reference to the MainViewModel.

Instead of maintaining a direct reference to the main view model and directly manipulating the book list, we instead publish a message (RemoveBookMessage). Any view model that is subscribing to that message, regardless of where it resides in the application, will be informed about this message when it is sent.

The following code from the constructor inside MainViewModel shows how we subscribe to the book removal message and perform the final book deletion without violating the separation between the two view models:

```
Messenger.Default.Register<RemoveBookMessage>(this, RemoveBook);
```

And then the implementation of the RemoveBook method performs the actual view model manipulation:

```
public void RemoveBook(RemoveBookMessage removeMessage)
{
    DeleteBookFromList(removeMessage.Book);
}
```

Worth pointing out here is that the only thing we have been manipulating up to this point has been the view model. When we get to the service provider topic, you’ll see how we can cleanly and elegantly wire this view model up to a backing or persistence store.