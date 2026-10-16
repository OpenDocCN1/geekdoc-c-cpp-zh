CultureInfo and SubCultures properties are assigned. With the result of this, a dictionary is created to enable fast access to the culture name.

For the data that should be bound, a list of CultureData objects is created that contains all the root cultures for the tree view after the foreach statement is completed. Root cultures can be verified to determine whether they have the invariant culture as their parent. The invariant culture has the Locale Identifier (LCID) 127. Every culture has its own unique identifier that can be used for a fast verification. In the code snippet, root cultures are added to the rootCultures collection within the block of the if statement. If a culture has the invariant culture as its parent, it is a root culture.

If the culture does not have a parent culture, it is added to the root nodes of the tree. To find parent cultures, all cultures are remembered inside a dictionary. (See Chapter 11, “Collections,” for more information about dictionaries, and Chapter 9, “Delegates, Lambdas, and Events,” for details about lambda expressions.) If the culture iterated is not a root culture, it is added to the SubCultures collection of the parent culture. The parent culture can be quickly found by using the dictionary. In the last step, the root cultures are made available to the UI by assigning them to the DataContext of the Window (code file WPFCultureDemo/MainWindow.xaml.cs):

```
private void SetupCultures()
{
	var cultureDataDict = CultureInfo.GetCultures(CultureTypes.AllCultures)
		.OrderBy(c => c.Name)
		.Select(c => new CultureData
		{
			CultureInfo = c,
			SubCultures = new List<CultureData>(())
		})
		.ToDictionary(c => c.CultureInfo.Name);

	var rootCultures = new List<CultureData>();
	foreach (var cd in cultureDataDict.Values)
	{
		if (cd.CultureInfo.Parent.LCID == 127)
		{
			rootCultures.Add(cd);
		}
		else
		{
			CultureData parentCultureData;
			if (cultureDataDict.TryGetValue(cd.CultureInfo.Parent.Name, out parentCultureData))
			{
				parentCultureData.SubCultures.Add(cd);
			}
			else
			{
				throw new ParentCultureException(
					"unexpected error—parent culture not found");
			}
		}
	}
}
```