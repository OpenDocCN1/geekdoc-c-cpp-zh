# The aspx code for the Cart page

Figure 3-20 shows the aspx code for the second page of the Shopping Cart application, Cart.aspx, which is rendered in figure 3-2. Once again, I’ve highlighted the start of each tag that defines a server control.

Here, the shopping cart is displayed in a ListBox control within an HTML table that allows the Remove and Empty buttons to be displayed to the right of the list box. These two buttons, as well as the CheckOut button, use an OnClick attribute to name the event handler that’s executed when the button is clicked. The Continue button uses the PostBackUrl attribute to return to the Order.aspx page. And the lblMessage label is used to display messages to the user. Like the Order page, this page also contains an image control that defines the image that’s displayed in the banner.

Notice here that the EnableViewState property of the label is set to False. That way, the value of this label isn’t maintained between HTTP requests. So if an error message is displayed in this label, it won’t be displayed again the next time the page is displayed.