# A list application that uses a ListView control

Now that you’ve learned the basic skills for working with a ListView control, the following topics present the design and code for an application that uses this control to display a list of products. If you compare this application with the list application in chapter 14 that uses a GridView control, you’ll begin to see the flexibility that the ListView control provides.

# The Product List application

Figure 16-8 presents the Product List application. Here, you can see that the first column in the ListView control contains the product name for each row in the Products table of the Halloween database. Then, the second column contains the headings for the other product columns that are included in the list, and the third column contains the data from each of the product columns. This type of layout wouldn’t be possible with the GridView control.

You should also notice the DataPager control that’s used with the ListView control. This control specifies that only four products should be displayed on each page. It’s implemented using a next/previous pager with custom values for the text that’s displayed on the buttons.