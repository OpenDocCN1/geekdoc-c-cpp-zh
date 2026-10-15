
Note that a few properties from each of the server controls have been defined in the resource file. For instance, the Button server control has its Text and ToolTip properties exposed in the resource file, and the Visual Studio localization tool has pulled the default Text property value from the control based on what you placed there. Looking more closely at the Button server control constructions in this file, you can see that both the Text and ToolTip properties have a defining Button1Resource1 value preceding the property name. This is the key that is used in the Button server control shown earlier.

In the following aspx source, a `meta:resourcekey` attribute has been added to a button control. In this case it references `Button1Resource1`. All the properties using this key in the resource file (for example, the Text and ToolTip properties) are applied to this Button server control at runtime.

```aspx
<asp:Button ID="Button1" runat="server" Text="Submit Name"
    meta:resourcekey="Button1Resource1" />
```

> *Code snippet from ProVB_Localization\Default.aspx*

## Adding Another Language Resource File

The `Default.aspx.resx` file created in the last section is used by the application as the default or invariant culture. No specific culture is assigned to this resource file. If for a given request no culture can be determined, then this is the resource file that is utilized. To add another resource file for the `Default.aspx` page that handles another language altogether, copy and paste the `Default.aspx.resx` file into the same `App_LocalResources` folder and rename the newly copied file. If you use `Default.aspx.fi-FI.resx`, give the following keys the values shown to make a Finnish-language resource file:

```text
Button1Resource1.Text     Lähetä Nimi
Label1Resource1.Text      Mikä sinun nimesi on?
PageResource1.Title       Näytesivu
```

Once you have created this file, take an additional step and create a custom resource in both resource files using the key `Label2Answer`. The `Default.aspx.resx` file should have the following new key:

```text
Label2Answer              Hello
```

Now you can add the key `Label2Answer` to the `Default.aspx.fi-FI.resx` file as shown here:

```text
Label2Answer              Hei
```

You now have resources for specific controls, and a resource that you can access later programmatically.

## Finalizing the Building of the Default.aspx Page

Finalizing the `Default.aspx` page, you want to add a `Button1_Click` event so that when the end user enters a name into the text box and clicks the Submit button, the `Label2` server control provides a greeting pulled from the local resource files. When all is said and done, your default page should have a code-behind element that matches the following code:

```vb
Partial Class _Default
    Inherits System.Web.UI.Page

    Protected Sub Button1_Click(ByVal sender As Object,
            ByVal e As System.EventArgs) Handles Button1.Click
        Label2.Text = GetLocalResourceObject("Label2Answer") &
            " " & TextBox1.Text
    End Sub
End Class
```

> *Code snippet from ProVB_Localization\Default.aspx.vb*

In addition to pulling local resources using the `meta:resourcekey` attribute in the server controls on the page to access the exposed attributes, you can also access any property value contained in the local resource file by using the GetLocalResourceObject. When using GetLocalResourceObject, you simply use the name of the key as a parameter, as shown here:

```
GetLocalResourceObject("Label2Answer")
```

With the code from the Default.aspx page in place and the resource files completed, you can run the page, entering a name in the text box and then clicking the Submit Name button to get a response, as shown in Figure 27-13.

What happened behind the scenes that caused this page to be constructed in this manner? First, only two resource files — Default.aspx.resx and Default.aspx.fi-FI.resx — are available. The Default.aspx.resx resource file is the invariant culture resource file, whereas the Default.aspx.fi-FI.resx resource file is for a specific culture (fi-FI). Because the browser requesting the Default.aspx page was set to en-US as the preferred culture, ASP.NET found the local resources for the Default.aspx page. From there, ASP.NET checked for an en-US-specific version of the Default.aspx page. Because there isn’t a specific page for the en-US culture, ASP.NET checked for an en-(neutral culture)-specific page. Not finding a page for the en neutral culture, ASP.NET was then forced to use the invariant culture resource file of Default.aspx.resx, producing the page shown in Figure 27-13.

If you now set your IE language preference as fi-FI and rerun the Default.aspx page, you’ll see a Finnish version of the page, as shown in Figure 27-14.

![](img/d99870e80390742f93963da7be0b2e61_922_0.png)

FIGURE 27-13

![](img/d99870e80390742f93963da7be0b2e61_922_1.png)

FIGURE 27-14

In this case, having set the IE language preference to fi-FI, you are presented with this culture’s page instead of the invariant culture page presented earlier. ASP.NET found this specific culture through use of the `Default.aspx.fi-FI.resx` resource file.

You can see that all the control properties that were translated and placed within the resource file are utilized automatically by ASP.NET, including the page title presented in the title bar of IE.

## Neutral Cultures Are Generally Preferred

When you are working with the resource files from this example, note that one of the resources is for a *specific culture*. The `Default.aspx.fi-FI.resx` file is for a specific culture — the Finnish language as spoken in Finland. Another option would be to make this file work not for a specific culture, but instead for a neutral culture. To do so, simply name the file `Default.aspx.fi.resx`. In this case, it doesn’t make a significant difference because no other countries speak Finnish; but it would make sense for languages such as German, Spanish, or French, which are spoken in multiple countries.

For instance, if you are going to have a Spanish version of the `Default.aspx` page, you could definitely build it for a specific culture, such as `Default.aspx.es-MX.resx`. This construction is for the Spanish language as spoken in Mexico. With this in place, if someone requests the `Default.aspx` page with the language setting of es-MX, that user is provided with the contents of this resource file. If the requester has a setting of es-ES, he or she will not get the `Default.aspx.es-MX.resx` resource file, but the invariant culture resource file of `Default.aspx.resx`. If you are going to make only a single translation for your site or any of your pages, construct the resource files to be for neutral cultures, not specific cultures.

If you have the resource file `Default.aspx.es.resx`, then it won’t matter if the end user’s preferred setting is set to es-MX, es-ES, or even es-AR — that user gets the appropriate es neutral-culture version of the page.

## Global Resources

Besides using only local resources that specifically deal with a particular page in your ASP.NET application, you also have the option to create *global resources* that can be used across multiple pages. To create a resource file that can be utilized across the entire application, right-click on the solution in the Solution Explorer of Visual Studio and select Add New Item. From the Add New Item dialog, select Resource File. Visual Studio prompts you to place this file in a new folder called App_GlobalResources. You’ll see that this file already exists in the sample code download. Once again, your first resource file is the invariant culture resource file. Add a single string resource with the key LabelText and assign a long string value to this key. The string “Non-Variant Format Label Text” was used in the code download. Next, add a third label control, Label3 to the bottom of your existing page.

Now that you have the invariant culture resource file completed, the next step is to add another resource file, but this time name it `Resource.es.resx`. Again, for this resource file, use a string key of LabelText and paste in the Spanish translation of the preceding text.

The point of a global resource file is to have access to these resources across the entire application. You can access the values that you place in these files in several ways. One way is to work the value directly into any of your server control declarations. For instance, you can place the following privacy statement in a Label server control as shown here:

```aspx
<asp:Label ID="Label3" runat="server"
    Text='<%$ Resources: Resource, LabelText %>'></asp:Label>
```

> *Code snippet from ProVB_Localization\Default.aspx*
