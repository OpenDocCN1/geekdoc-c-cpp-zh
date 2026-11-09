+   17. Select the XML File option from the middle pane (Fig ASP-2.69).
+   18. Enter the name in the Name text box, say **AddFile.xml**, and click the Add button to add the file in a project, as shown in Fig.ASP-2.69.

![](bbox=[0.214, 0.188, 0.368, 0.401])

![](bbox=[0.421, 0.188, 0.809, 0.401])

The XML file appears with the name **AddFile.xml**

19. Add the code given in Listing 2.13 in the **AddFile.xml** file:

# **Listing 2.13: Illustrating the Code for the AddFile.xml File**

```
<Advertisements>
    <Ad>
        <ImageUrl>~/Images/Chrysanthemum.jpg</ImageUrl>
        <NavigateUrl>http://www.google.com</NavigateUrl>
        <AlternateText>Visit Google.com</AlternateText>
        <Impressions>80</Impressions>
        <Keyword>search</Keyword>
    </Ad>
    <Ad>
        <ImageUrl>~/Images/Desert.jpg</ImageUrl>
        <NavigateUrl>http://www.msn.com</NavigateUrl>
        <AlternateText>
            Visit MSN.com
        </AlternateText>
        <Impressions>80</Impressions>
        <Keyword>MSN</Keyword>
    </Ad>
    <Ad>
        <ImageUrl>~/Images/Hydrangeas.jpg</ImageUrl>
        <NavigateUrl>http://www.yahoo.com</NavigateUrl>
        <AlternateText>
            Visit yahoo.com
        </AlternateText>
        <Impressions>80</Impressions>
        <Keyword>yahoo</Keyword>
    </Ad>
</Advertisements>
```

The preceding code defines the following tags:

+   - **<Advertisements>:** Refers to the opening tag of the XML file.
+   - **<Ad>:** Refers to the tag that is used for each image. In Listing 2.13, we have used three images, so there are three `<Ad>` tags.
+   - **<ImageUrl>:** Specifies the path of the image. There is one `<ImageUrl>` tag for each image.
+   - **<NavigateUrl>:** Notifies the URL, where the image will navigate after the click event.