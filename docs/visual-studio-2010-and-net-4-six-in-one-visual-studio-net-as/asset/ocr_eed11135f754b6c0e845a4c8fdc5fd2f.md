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

> Code file [4-ServerSideData?7-DataContextReadWrite.htm] available for download at Wrox.com

At this point, you can refresh the page, modify any record, and then click on the "Save changes" button to initiate an update in the background, which will obviously fail, because you do not have the web method on the server. However, you can use `Fiddler` or `Firebug` to examine the body of this POST request.