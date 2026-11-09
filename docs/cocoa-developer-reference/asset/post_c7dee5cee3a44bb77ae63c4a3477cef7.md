
**Figure 14.4** Naming an entity. Note that the Inspector pane also lists the entity's class. The `NSManagedObject` class is a special wrapper class used by Core Data.

![](img/2b293e29fc15b0797f113b85dd429b6e_376_0.png)

## Adding properties

Next, you'll add some properties to the Album entity. Click the + icon at the bottom left of the Property pane, and select Add Attribute, as shown in Figure 14.5. Type Name into the name field in the Inspector window. Deselect Optional. Select String from the Type pop-up menu. This adds a new property called Name, which is a string, and must be present. Repeat the steps to add another property. Name it Year. Set its Type to Date and deselect Optional.

**Figure 14.5** Adding a property. Use the Inspector pane to set the name and type. Deselecting Optional means that the property must be set. (Note: This image is a composite showing both menus.)

![](img/2b293e29fc15b0797f113b85dd429b6e_377_0.png)

Create another entity called Artist. Add a nonoptional property called Name. The model graph should look like Figure 14.6.

## Creating relationships

A relationship is a link between one entity and another. Relationships are used to pull data out of associated entities. They define properties indirectly.

In this example, Albums are created by Artists, so there needs to be a relationship between the Album and Artist entities. There should also be a relationship in the other direction, because Artists can record more than one Album.

**Figure 14.6** Your model is starting to take shape, with two entities.

![](img/2b293e29fc15b0797f113b85dd429b6e_378_0.png)

A relationship from one object to multiple objects is called a *to-many relationship* — one entity is connected to many others. Unlike a full relational database, Core Data’s support for to-many relationships is limited.

To illustrate this, you'll create the Album ⇔ Artist relationship as a to-one, and the Artist ⇔ Album relationship as a to-many.

Select the Album entity, and click the + icon at the bottom left of the Property pane. Select Add Relationship from the pop-up menu, as shown in Figure 14.7. Name the relationship **Artist**. Deselect Optional. In the Destination pop-up, select Artist. The editor automatically adds an arrow linking the two entities.

**Figure 14.7** Creating and defining a relationship. The arrow appears automatically.

![](img/2b293e29fc15b0797f113b85dd429b6e_379_0.png)

![](img/2b293e29fc15b0797f113b85dd429b6e_379_1.png)

> **NOTE**
>
> Although the editor is visual, the layout of the model on the graph isn’t important. Names and properties are important, and so is the fact that a relationship exists. But you can move entities to different locations on the graph without affecting either.

Repeat the process for the Artist entity, creating a relationship to Album, as shown in Figure 14.8. Selecting Artist in the Inverse pop-up menu creates a two-way relationship and replaces two arrows with a single arrow with arrowheads at both ends.

**Figure 14.8** Creating a reciprocal relationship. The two entities are now connected in both directions.

![](img/2b293e29fc15b0797f113b85dd429b6e_379_2.png)

![](img/2b293e29fc15b0797f113b85dd429b6e_380_0.png)

> **TIP**
>
> The double arrowhead indicates a to-many relationship. The single arrowhead indicates a to-one relationship.

## Generating a user interface

Interface Builder can take a Core Data entity and build an interface for it. This feature is very easy to use and generates a default nib file that you can customize to taste. Bindings are included to link objects in the UI to the objects managed by Core Data.

Open the Resources Group, and double-click MainMenu.xib. Open the Document window if it isn't already visible. Double-click the Window object to open its edit window. Press Option-drag the Album entity and release it on the empty edit window. You'll see the dialog shown in Figure 14.9. Select the Master/Detail view option from the pop-up menu, and select all the boxes. When the next dialog appears, leave the property boxes and select Finish.

> **TIP**
>
> This is very much easier with two monitors. If you have a single monitor, you'll have to resize Xcode and Interface Builder to fit both onto the screen at the same time.

**Figure 14.9** Creating a Core Data interface in IB. The check boxes define the elements that appear in the interface.

![](img/2b293e29fc15b0797f113b85dd429b6e_381_0.png)

IB adds the UI shown in Figure 14.10 to the window. Any properties that are included in the source entity will appear here as text fields. To-one relationships linked to other entities generate a pop-up. As you can see at the left, this is a standard nib file. You can move elements around, add autosizing, and so on.

Make the window much wider to add another UI panel, and then press Option+drag the Artist entity into the window. Make the same selections as before to create another Master-Detail view showing the Artist properties. The finished UI is shown in Figure 14.11. You won’t see a pop-up menu for albums, because the UI doesn’t support to-many relationships. This simple UI isn’t intelligent enough to allow to-many editing.

**Figure 14.10** The auto-generated user interface for the project, with its associated nib.

![](img/2b293e29fc15b0797f113b85dd429b6e_382_0.png)

> **TIP**
>
> The new panel appears in the middle of the window, overlapping the original panel. If you mis-click while trying to drag it, it can be difficult to select it again. The easy way to select it before moving it is to double-click the Box (Artist) element in the Doc window.

## Building the application

Once the UI is complete, save the nib file and Build and Run the application. No code is needed! The completed application is shown in Figure 14.12. Click the Add button to add some artists, then add some albums in the same way. Use the Artist pop-up menu to select the artist name for each album. You can also click the entries under the Artist column directly.

**Figure 14.11** Adding another panel for the Artist entity. Repositioning this panel can be tricky.

![](img/2b293e29fc15b0797f113b85dd429b6e_383_0.png)

**Figure 14.12** The finished application with some sample data

![](img/2b293e29fc15b0797f113b85dd429b6e_383_1.png)

The design is rough around the edges, but it supports the following features:

- **Input checking.**
- **Editing.** You can change any entry.
- **Sorting.** Click the column headers.
- **Searching.** Type into the search bar.
- **Save and reload.** Choose File ▷ Save to save the data. Data is reloaded automatically.
- **OS X standard undo.**

This is impressive without code; but it does have some limitations:

- **The date field** shows the day, date, and time, when it should only show the year.
- **Links are unidirectional.** It would be useful to filter the albums by artist.

![](img/2b293e29fc15b0797f113b85dd429b6e_384_0.png)

> **CAUTION**
>
> Core Data can't reload previously saved data if you change the model; if you try this, the application will crash. A feature called migration can repair entities programmatically, but migration is an advanced topic and is beyond the scope of this book.

## Exploring and Extending a Core Data Application

You can improve on this application in two ways: by modifying the nib and by adding code to implement custom features. Take a closer look at the application nib, shown in Figure 14.13.

The format is similar to the table view example from the previous chapter. The Album box includes a table view with three column objects. Each is bound to a separate key in the Album Array Controller object. This generates the three column views.

Each array controller is bound to the managedObjectContext in the App Delegate, as shown in Figure 14.14. This is Core Data’s main data store. The managed object context binding option includes features that search the store automatically, returning arrays of values and keys that can be displayed by an array controller.

Expanding the Year column reveals that the Year field already includes a date formatter object. A date formatter is similar to the NSDateFormatter object introduced in the previous chapter. You can use it to control how dates are displayed.
