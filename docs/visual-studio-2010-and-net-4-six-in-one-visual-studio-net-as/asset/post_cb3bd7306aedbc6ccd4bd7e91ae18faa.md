
The browser will render textboxes as shown in Figure 19-14.

| Name | Capital |
|---|---|
| Name: Australia | Capital: Canberra |
| Name: Austria | Capital: Vienna |
| Name: Brazil | Capital: Brasil |
| Name: Croatia | Capital: Zagreb |
| Name: Finland | Capital: Helsinki |
| Name: Greece | Capital: Athens |
| Name: Hungary | Capital: Budapest |
| Name: Slovakia | Capital: Bratislava |
| Name: Spain | Capital: Madrid |
| Name: Sweden | Capital: Stockholm |
| Name: United Kingdom | Capital: London |
| Name: United States | Capital: Washington, D.C. |

**FIGURE 19-14:** Using two-way binding to update data

To support updates, you must set the name of the update method in the `saveOperation` property.

```
dataContext = Sys.create.dataContext(
  serviceUri: "../Services/CountryService.asmx",
  saveOperation: "UpdateCountries"
);
```

> Code file [4-ServerSideData?7-DataContextReadWrite.htm] available for download at Wrox.com.

In this case, the `UpdateCountries` method is used for updating countries. However, its signature is not null. The `Sys.Observer` automatically takes care of all change tracking in the background by using it to provide a changeset that contains only the inserted, modified, and updated items. If you want to send this changeset to the server, you can call the `saveChanges` method that will call the `saveOperation` web method. The only question is, exactly what is posted by the client to the server?

Add a button to the GUI to let the user post changes to the server:

```
<input type="button" value="Save changes" onclick="dataContext.saveChanges() />
```

> Code file [4-ServerSideData?7-DataContextReadWrite.htm] available for download at Wrox.com.

At this point, you can refresh the page, modify any record, and then click on the "Save changes" button to initiate an update in the background, which will obviously fail, because you do not have the web method on the server. However, you can use `Fiddler` or `Firebug` to examine the body of this POST request.

For example, if you change "United Kingdom" to "UK," and "United States" to "US," the DataContext will send the following JSON data to the server (the code has been broken into more lines to make it more readable):

```
{
  "changeSet": [
    {
      "action":1,
      "item": {
        "__type":"Country",
        "Name":"UK",
        "Code":"uk",
        "Capital":"London"
      }
    },
    {
      "action":1,
      "item": {
        "__type":"Country",
        "Name":"US",
        "Code":"us",
        "Capital":"Washington, D.C."
      }
    }
  ]
}
```

The client sends a single changeSet object to the server that is an array of change objects. Every change object has two properties:

- action — This property describes what happened to the specified item. This property has one of the following Sys.Data.ChangeOperationContext values: insert (0), update (1) or remove (2).
- item — This property carries the modified records. As you can see, there is no explicit identity or previous value. It is up to you to determine which was the original item and how the properties are changed.

Actually, the changeset contains Sys.Data.OperationContext instances that can have more properties, but in this scenario, only the action and the item properties are used.

Now that you have change to send by the client, you can prepare to receive it on the server. First, mirror the ChangeOperationType enum in C#:

```
public enum ChangeOperationType { insert, update, remove }
```

![](img/b5597c749e848b27b0d305153ae16106_927_0.png)

Code file [App.Code\Code\Change.cs] available for download at Wrox.com.

Then, create a generic Class to mimic the change records sent by the client, with an action and an item property:

```
public class Change<T>
{
    public ChangeOperationType action;
    public T item;
}
```

![](img/b5597c749e848b27b0d305153ae16106_928_0.png)

Code file [App_Code_Change.cs] available for download at Wrox.com.

Now, you have everything to implement the UpdateCountries method that is set as the saveOperation for the DataContext:

![](img/b5597c749e848b27b0d305153ae16106_928_1.png)

```
[WebMethod]
public void UpdateCountries( List<Change<Country>> changeSet)
{
    foreach (Change<Country> change in changeSet)
    {
        switch (change.action)
        {
            case ChangeOperationType.insert:
                // Implement insert here...
                break;
            case ChangeOperationType.update:
                this.UpdateCountry(change.item);
                break;
            case ChangeOperationType.remove:
                // Implement remove here...
                break;
        }
    }
}
```

Code file [App_Code_CountryService.cs] available for download at Wrox.com.

Because the client sends an array, you can use a generic list as a method parameter, iterate through the records, and examine what happened with them. The previous code snippet implements only the update operation branch, because the client supports only updating so far. Updating a country is delegated to the private UpdateCountry method:

```
private void UpdateCountry(Country newCountry)
{
    Country oldCountry = CountryService.countries.Where(
        c => c.Code == newCountry.Code ).First();
    oldCountry.Name = newCountry.Name;
    oldCountry.Capital = newCountry.Capital;
}
```

![](img/b5597c749e848b27b0d305153ae16106_928_2.png)

Code file [App_Code_CountryService.cs] available for download at Wrox.com.

Remember, the server-side "data store" is implemented as a private list in CountryService. So, in this case, it is easy to persist the changes.

In addition to updating, the DataContext also supports insertions and deletions. To add a new item to the entity, you can call the insertEntity and removeEntity method. It is often requested that the cache be refreshed from the server, and you can complete this by calling the fetchData method of the DataView — for example, in a click handler of a button:

```
<input type="button" value="Refresh from server" onclick="$(CountryList).fetchData(null, null,Sys.Data.MergeOption.overwriteChanges)" />
```

![](img/b5597c749e848b27b0d305153ae16106_929_0.png)

Code file [4-ServerSideData7-DataContextReadWrite.cs] available for download at Wix.com

Because the data on the client is already tracked, it is important to define how the data on the client and from the server should be merged. You can set this with a Sys.Data.MergeOption value in the third parameter. If you set MergeOption.appendOnly, changes are preserved on the client, and will not be overwritten by the data from the server. If you set MergeOption.overwriteChanges, then values obtained from the server will overwrite the ones on the client.

As you can see, the DataContext is a very complex object with convenient usage. You can use it in even simpler-client code: just pass your object to its trackData method, and the full power of the tracking engine is added to your object.
