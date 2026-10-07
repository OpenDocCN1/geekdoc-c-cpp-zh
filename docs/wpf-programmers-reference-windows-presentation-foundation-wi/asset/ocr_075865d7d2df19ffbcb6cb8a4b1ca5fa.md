# 382 | CHAPTER 22 NAVIGATION-BASED APPLICATIONS

```
NavigateUri="http://thesaurus.reference.com/*">Thesaurus.com</HyperLink>
</Paragraph>
<List>
<ListItem>
<Paragraph>
<HyperLink>
NavigateUri="http://dictionary.reference.com/*">Dictionary.com</HyperLink>
<LineBreak/>
</Paragraph>
</ListItem>
<ListItem>
<Paragraph>
<HyperLink>
NavigateUri="Page2.xml*">Map Links</HyperLink>
</Paragraph>
</ListItem>
</List>
</FlowDocument>
```

PageDocument

The Page holds a FlowDocument object that contains everything else. The document holds a paragraph followed by a list.

Each item contains a paragraph that holds a Hyperlink object. The Hyperlink's NavigateUri attribute tells the Page where to go when the user clicks the link.

Most of the links lead to web addresses, but the last one has NavigateUri set to "Page2.xml". When the user clicks on this hyperlink, the program creates a new Page2.xml object and navigates to.

# RECYCLING OLD OBJECTS

> It is important to note that navigating to a new instance of a Page rather than reusing any existing Page objects. In contrast, if you click the Back or Next to move to a previously viewed Page, the program redraws the object it previously showed.

For example, a program's first Page contains a TextBox. You enter text into it and click on a hyperlink to move to a second Page. Now, if you click the Back-button, you will see the text on the first Page. However, if you click on another hyperlink to move to the first Page, you'll see a new object with a blank textbox.

If you want to allow this sort of navigation but the hyperlink to lead to the original Page object, you'll need to use some code-behind rather than letting the hyperlink navigate for you automatically.

# NAVATIONSSERVICE

In addition to using hyperlinks, an application's code-behind can use a NavigationService to navigate. A NavigationService object lets an application code-behind to control how the container navigates.