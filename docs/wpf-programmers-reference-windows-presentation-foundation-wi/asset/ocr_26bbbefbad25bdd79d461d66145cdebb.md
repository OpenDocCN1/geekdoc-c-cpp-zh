# Hyperlink Navigation | 38

The Width and Height properties determine how big the Page is within its container. The WindowWidth and WindowHeight properties determine how big the container is initially.
The unnamed Border Style modifies the Page so that it displays its thick red border.

# NO NAVIGATIONNEEDED

If you run an application that uses a Page as its startup object, the program displays the Page in a NavigationWindow that provides the Back and Next buttons. Normally, you display a Page either in this way or by placing it inside a Frame control.

# HYPERLINK NAVIGATION

One simple way to navigate in a Page is to document it that it contains hyperlinks. The hyperlinks automatically navigate from the application's Pages and even to external locations on the Web.

The PageDocument example program shown in Figure 2-2 contains two Pages. Each Page displays a FlowDocument that contains a series of hyperlinks that let you to navigate between sites. The bottom link on each Page leads to the other Page.

Figure 22-2 shows the navigation dropdown open and displaying the program's navigation history. When I started the program, it displayed its Writing Links. I used the hyperlinks to navigate to the Map Links page (displayed as "Current Page" in the dropdown) and then to the Google Maps. Next, I clicked on the Back button to move back to the Map Links page and opened the dropdown. The mouse is over the Writing Links page so it is highlighted and displays a left arrow. Figure 22-2. ("Future" pages such as Google Maps in this case display a right arrow). The second page is similar.

The following code shows the body of the program's first.

```
<FlowDocument>
<Paragraph FontSize="20" FontWeight="Bold" TextAlignment="Center">
  Writing Links
</Paragraph>
<List>
  <ListItem>
    <Paragraph>
      <Hyperlink NavigateUri="http://www.rhymezone.com/">RhymeZone</Hyperlink>
    </Paragraph>
  </ListItem>
  <ListItem>
    <Paragraph>
      <Hyperlink>
    </Paragraph>
  </ListItem>
</List>
</FlowDocument>
```

![](bbox=[0.613, 0.373, 0.882, 0.584])

FIGURE 22-2

Available for download on Wrox.com