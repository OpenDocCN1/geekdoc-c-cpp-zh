
```
public string Title
{
    get
    {
        return title;
    }
    set
    {
        title = value;
        RaisePropertyChanged("Title");
    }
}

public string Description
{
    get
    {
        return description;
    }
    set
    {
        description = value;
        RaisePropertyChanged("Description");
    }
}

private void InitializeCommands()
{
    // when someone uses a context menu to delete THIS book,
    // broadcast a message so any affected viewmodels
    // can handle it (e.g the global book list)
    RemoveBookCommand = new RelayCommand(
        () =>
            Messenger.Default.Send<RemoveBookMessage>(
                new RemoveBookMessage(this)));
}
}
```

RelayCommand is a class that comes with the MVVM Light framework. This class provides a wrapper for code that will be executed when the command is executed. In addition, it also provides a wrapper for code that will be executed to determine whether a command is executable. When you bind regular buttons to commands, they will run the custom code in the RelayCommand that returns a true or false. When the code returns false, the button will be disabled.

To summarize, commands provide a way to bind UI elements declaratively to a reusable wrapper around a block of code. These commands can be bound using Blend or Visual Studio 2010’s designer or by typing the XAML in by hand. Again, I like to keep things declarative as long as possible, so I’m a huge fan of using commands to react to UI events whenever possible.

There is one spot in WP7 that isn’t compatible with commands: the application bar. The application bar controls aren’t real Silverlight controls and, despite efforts to make them look like real controls, they don’t behave the same way Silverlight controls behave. This is because the application bar exists outside the application’s main frame and can shrink or grow the application based on the opacity setting of the app bar. With the application bar menu items, you’re still going to have to respond to the click event. However, that doesn’t mean you have to embed code directly in the code-behind; you can forward that click to a command. In the following code, I forward the click from the Add button on the app bar to a command that adds books to the main view model:

```
private void addBookButton_Click(object sender, System.EventArgs e)
{
    var vm = DataContext as MainViewModel;
    if (vm != null)
    {
        vm.AddBookCommand.Execute(null);
    }
}
```

Finally, at the bottom of Listing 16.2 you might have noticed the Messenger.Default.Send code. By sheer coincidence, this leads me to my next topic: messaging.

## Sending Messages with MVVM Light

When trying to maintain a clear separation of concerns, one of the hardest things to do is avoid making direct method calls on dependent objects. The reason this is a problem is that every time you do this, you string another piece of spaghetti between two layers of your application and eventually, that spaghetti becomes so hard to untangle (without breaking) that the only way to maintain your application is to just keep heaping more meatballs on top.

Messaging is another way of maintaining a clear separation of concerns as well as ensuring that all the actors in your MVVM application stick to the script. Messaging (also referred to as “pub/sub” or just “pub sub” by many) allows components of your application to advertise when important things happen without actually knowing ahead of time what needs to take place in response. This decouples the pieces of your application that are performing notable events from the pieces that respond to them.

In Listing 16.2, you saw the following code that creates an instance of the RemoveBookCommand object:

```
RemoveBookCommand = new RelayCommand(
    () => Messenger.Default.Send<RemoveBookMessage>(
        new RemoveBookMessage(this));
```

In this code I’m saying that every time the RemoveBookCommand is executed (regardless of how or why it is executed) that the current view model (Book) will send a message to all subscribers indicating that a book has been marked for removal.

Why not just make sure that each instance of the Book view model has a reference to the MainView model? This way the book could just remove itself directly from the list. The problem with this pattern is that it violates the “don’t look up” principal of MVVM development, and it means that anytime we want any other view model to respond to the deletion of a book, we have to put that code in the Book view model rather than in the appropriate view models.

## Don’t Look Up

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

## Look Ma, No Code-Behind!

Another thing that you can do with messaging is combine it with the notification of property changes. This allows you to notify other view models automatically when properties change, essentially extending the reach of the standard property change notification system to MVVM Light's message “bus”.

To show you how to do that, I will walk you through a solution to a classic problem in applications that need to maintain clear separation of concerns: transitioning between pages. For our sample application, when users tap on a book, they will be taken to another page. This page contains a pivot view that lets the user flip through the characters, places, plots, inspirations, and scenes for that book.

How do you transition from one page to another when tapping on an item should be handled by the view model and not the code-behind? Isn’t it a violation of concern separation to directly instantiate the details page from the master page and navigate to it? This particular debate will probably rage on for hundreds of years, but my personal view is that if I can avoid a direct coupling between the pages, I will.

Take a look at the XAML for the declaration of my list box:

```
<ListBox x:Name="bookListBox"
ItemsSource="{Binding Books}"
ItemTemplate="{StaticResource bookItemTemplate}"
SelectedItem="{Binding Path=SelectedBook, Mode=TwoWay}">
</ListBox>
```

What I’ve done here is bind the SelectedItem property of the list box to a property I have in my view model called SelectedBook. This binding is bidirectional so I can affect the UI by changing the value from the code, or the UI can affect my code when the user taps an item. Here’s the definition of my SelectedBook property:

```
public Book SelectedBook
{
    get
    {
        return selectedBook;
    }
    set
    {
        var oldValue = selectedBook;
        if (oldValue == value) return;
        selectedBook = value;
        // broadcast this to all listening viewmodels, not just bound UI
        RaisePropertyChanged("SelectedBook", oldValue, selectedBook, true);
        this.SelectedBook = null;
    }
}
```
