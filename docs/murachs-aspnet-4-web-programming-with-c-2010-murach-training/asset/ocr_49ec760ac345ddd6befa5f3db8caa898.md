# # How to enable paging

Paging refers to the ability of the GridView control to display bound data one page at a time, along with paging controls that let the user select which page of data to display next. As figure 14-5 shows, the GridView control lets you enable paging simply by setting the AllowPaging attribute to True.

When you enable paging, an additional row is displayed at the bottom of the GridView control to display the paging controls. If you want, you can provide a PagerStyle element to control how this row is formatted. In the example in this figure, the PagerStyle element specifies that the background color for the pager row should be light gray and the pager controls should be horizontally centered.

Unlike sorting, the GridView control doesn’t delegate the paging function to the underlying data source. Like sorting, however, paging works only for data sources that are in DataSet mode.