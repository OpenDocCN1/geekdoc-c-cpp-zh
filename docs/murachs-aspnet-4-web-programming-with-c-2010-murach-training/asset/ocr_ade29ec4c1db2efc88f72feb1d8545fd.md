# How to enable paging

Like the GridView control, the DetailsView control supports paging. As figure 15-3 shows, a row of paging controls is displayed at the bottom of the DetailsView control when you set the AllowPaging attribute to True. Then, you can specify the paging mode by including a PagerSettings element, and you can include PagerStyle and PagerTemplate elements to specify the appearance of the pager controls.

Note that if the data source contains more than a few dozen items, paging isn’t a practical way to provide for navigation. In most cases, then, a DetailsView control is associated with a list control that is used to select the item to be displayed. You’ll learn how to create pages that work this way in the next figure.