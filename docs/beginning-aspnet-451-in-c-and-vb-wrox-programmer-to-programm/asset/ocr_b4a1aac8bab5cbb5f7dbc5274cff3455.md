# C#

```
FirstName = Profile.FirstName;
```

Retrieving properties in a group is almost identical. To access the Street property discussed in a previous example, you will need this code:

# VB.NET

```
PostalAddressStreet.Text = Profile.PostalAddress.Street
```

# C#

```
PostalAddressStreet.Text = Profile.PostalAddress.Street;
```

Accessing the FavoriteGenres property is slightly different. Because this property is a collection, you shouldn't assign a value to it directly. Instead, use its methods and properties to get data in and out. The following example clears the entire list, and then adds the IDs of two genres to it:

# VB.NET

```
Profile.FavoriteGenres.Clear()
Profile.FavoriteGenres.Add(7)
Profile.FavoriteGenres.Add(11);
```

# C#

```
Profile.FavoriteGenres.Clear();
Profile.FavoriteGenres.Add(7);
Profile.FavoriteGenres.Add(11);
```

The following exercise shows how to store basic data in the user's profile. You will see a real-world implementation using the FavoriteGenres list in a later exercise.

# TRY IT OUT Storing Basic User Data in the Profile

In this It Out, you modify the Profile page to save their first and last name, birthday, and a short biography in their profile.

+   1. Open MyProfile.aspx again and switch to Code Behind. Remove the two lines of code in Page_Load that set the first and last name.

+   2. Switch to Design View and position your cursor between the paragraph and the ChangePassword control. To position your cursor, click the ChangePassword once to select it, and press the left arrow key. Add an TextBox table of five rows and three columns by choosing Table ⇞ Insert Table.

+   3. In the second column of each of the four rows, drag TextBox controls and rename them, from the first to the last row, FirstName, LastName, DateOfBirth, and Bio by setting their ID attribute. Figure 17-3 shows you exactly where the TextBox controls should be placed.

+   4. In the first column of each of the four rows, drop Label controls and set their properties follows so each label is associated with a TextBox in that row.