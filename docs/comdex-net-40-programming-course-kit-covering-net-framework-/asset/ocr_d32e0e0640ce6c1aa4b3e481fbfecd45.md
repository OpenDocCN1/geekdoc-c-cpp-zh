The preceding code snippet displays the current selected date and time in **TextBox1**.

+   16. Press the F5 key to run the application and select current date. The selected date is displayed in **TextBox1**, as shown in Fig.ASP-2.63:

![](bbox=[0.351, 0.189, 0.671, 0.398])

Fig.ASP-2.63

Let’s now discuss the **AdRotator** control.

# ## Using the AdRotator Control

The AdRotator is an ASP.NET control that is used to display a sequence of images, known as advertisement, on a Web page. These images are displayed in a random order and change when a user clicks the refresh button. The AdRotator control advertisements are associated with links; therefore, when you click on an advertisement, it redirects the control to the link page. It is associated with a data source, which is normally an xml file or a database table. A data source contains all the information, such as advertisement graphics reference, link, and alternate text. Therefore, when you use the AdRotator control, first create a data source, such as an .xml file or a SQL table, which contains all the information, and then associate the AdRotator control with the data source.

Noteworthy properties of AdRotator control are listed in Table 2.20:

**Table 2.20: Noteworthy Properties of the AdRotator Control**

| Property | Description |
|---|---|
| `AdvertisementFile` | Obtains or sets the path to an XML document that contains advertisement information |
| `AlternateTextField` | Obtains or sets a custom data field to use in place of the `AlternateText` attribute for an advertisement |
| `ImageUrlField` | Obtains or sets a custom data field to use in place of the `ImageUrl` attribute for an advertisement |
| `KeywordFilter` | Obtains or sets a category keyword to filter for specific types of advertisements in the XML advertisement file |
| `NavigateUrlField` | Obtains or sets a custom data field to use in place of the `NavigateUrl` attribute for an advertisement |
| `Target` | Obtains or sets the mode of the URL open, which you provide in `NavigateUrlField`, such as the URL should open in a new window or same window. |
| `UniqueID` | Obtains the unique, hierarchically qualified identifier for the AdRotator control |