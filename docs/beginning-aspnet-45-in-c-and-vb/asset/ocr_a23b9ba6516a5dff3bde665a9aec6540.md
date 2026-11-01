To define properties, you use <add> elements with a name attribute and an optional type if the property is of a type other than System.String. For example:

```
<add name="FavoriteGenres" type="System.Collections.Generic.List`1[System.Int32]" />
```

This property sets up a list that can store Integer values to hold the user's favorite music genres. You see how to use this property in a later exercise.

After you have set up the profile in Web.config and the background class has been compiled, you can access the profile in your pages. For example, you can now set properties such as FirstName through code:

```
VB.NET
Profile.FirstName = "Your first name here"
```

```
C#
Profile.FirstName = "Your first name here";
```

Although not used in this exercise, you access properties in a group in pretty much the same way. All you need to do is prefix the property name with the group name and a dot. Given the example of a PostalAddress, you would store the street for that address like this:

```
VB.NET
Profile.PostalAddress.Street = "Some Street"
```

```
C#
Profile.PostalAddress.Street = "Some Street";
```

Changes made to the profile are saved automatically for you during EndRequest, an event that fires very late during the ASP.NET page life cycle. This way, you can change the profile during many of the stages of the life cycle without having to worry about explicitly saving the profile manually.

In Figure 17-2, you can see how a single row is used to store the entire profile. The first column contains the unique ID of the user to which the profile belongs. The second column contains a list of property names that are saved for the current user, together with a starting index of the value and a length. For example, for the last name you see:

```
LastName:4:10
```

This states that the value for the LastName property, which is stored in the PropertyValueStrings column, starts at position 4 (the fifth character because zero-based positions are used) and has a length of 10 characters. This dense format enables the Profile provider to store many different properties in a single column, which eliminates the need to mess with the database schema any time the profile changes. Earlier versions of the Profile provider used the PropertyValueBinary column to store binary objects such as images. However, the Profile provider converts these to strings and stores them in the PropertyValueStrings column as well.