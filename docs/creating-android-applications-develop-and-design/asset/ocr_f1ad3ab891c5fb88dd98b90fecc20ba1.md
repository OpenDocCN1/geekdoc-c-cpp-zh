# REACTING TO CLICK EVENTS

Your code will need to listen for item clicks.

What's the point of having a menu if you can't tell when items have been selected? Right, there isn't one. Let me show you the final piece to my basic list menu example. Add the following method to your MainMenuActivity.java file:

```
@Override
public void onListItemClick(ListView lv,
        View clickedView,
        int position, long id)
{
    super.onListItemClick(lv, clickedView, position, id);
    TextView tv = (TextView)clickedView;
    Toast.makeText(getApplicationContext(),
        "List Item "+tv.getText()+" was clicked!",
        Toast.LENGTH_SHORT).show();
}
```

The ListActivity will call this method (if you've defined it) every time an element in the list view is clicked (or tapped with a finger). For more-complicated lists, you may want to use the ID (especially if you are using SQLite as a backing store). For this simple demo, I've just popped up a little dialog showing the text of the item that was pressed. If you're implementing your own basic main menu, I suggest you use the position of the clicked item to start an activity, service, or other action. You can see an example of this if you look at the associated source code.

That's the most basic list view I could possibly show you. Now, I'll take you in the opposite direction and show you what a custom list backed by a remote data source looks like.