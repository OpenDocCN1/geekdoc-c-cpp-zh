9. Save all your changes, request the Profile page in your browser, and log in when required. You should see the list of genres displayed in the browser, each one preceded by a check box. Select a couple of your favorite genres and click the Save Profile button. Browse to another page and choose My Profile again from the main Menu or TreeView. The genres you selected should still be selected in the page, as shown in Figure 17-7.

# How It Works

Earlier you defined the FavoriteGenres property in the profile as a generic list that can hold integer values. Because this property is a List, you do not assign values to it directly; instead, you use its methods like Add and Clear to add and remove items. Because each genre ID should be stored in the list only once, the list is cleared to remove any selection made earlier and then the selected items are added again:

```
VB.NET
Profile.FavoriteGenres.Clear()
```

```
C#
Profile.FavoriteGenres.Clear();
```

Then when the list is empty, the IDs of the selected genres are added:

```
VB.NET
For Each myItem As ListItem In PreferenceList.Items
    If myItem.Selected Then
        Profile.FavoriteGenres.Add(Convert.ToInt32(myItem.Value))
    End If
Next
```

```
C#
foreach (ListItem myItem in PreferenceList.Items)
{
    if (myItem.Selected)
    {
        Profile.FavoriteGenres.Add(Convert.ToInt32(myItem.Value));
    }
}
```

This code loops through all the items in the CheckBoxList. The Selected property determines whether the user has selected the item in the Profile page. If it has been selected, the value of the genre is retrieved, converted to an Integer (an int in C#), and then added to the FavoriteGenres list using the Add method.

![](bbox=[0.65, 0.2, 0.9, 0.55])