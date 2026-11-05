Master pages actually consist of two pieces: the master page itself and one or more content pages. Individual content pages contain the content you want to display in the context of the master page template. When users request the content pages, the master page is merged with the content page to produce output that combines the layout of the master page with the new material from the content page. The content pages associated with the master page for the DynamicPage example are About.aspx and Default.aspx.

The other major difference between a master page and content pages like Default.aspx and About.aspx is that the master page has one or more ContentPlaceHolders defined with an ID. These placeholders define areas where replaceable content will appear. HeadContent and MainContent ContentPlaceHolders are shown on Lines 9 and 44 in Figure 15-7. Figures 15-8 and 15-9 show the replaceable content for the About.aspx and Default.aspx pages.

![](bbox=[0.17, 0.41, 0.86, 0.75])

Figure 15-8    MainContent in the About.aspx page

Lines 6 through 13 provide the content for the MainContent ContentPlaceHolders in Figures 15-8 for the About page. The static text "About" and "Put content here" is the content used to fill the white area (MainContent) on the page. As you review Figure 15-9, notice the content for MainContent is defined on lines 6 through 19 for the Default.aspx page.