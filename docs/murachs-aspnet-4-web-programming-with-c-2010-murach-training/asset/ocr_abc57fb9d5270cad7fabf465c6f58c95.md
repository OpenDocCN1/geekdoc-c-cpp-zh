the validators on this page work properly. Then, enter customer information in the text boxes and click the Continue Shopping button again. Add another item to the cart and click the Check Out button again. This time, the customer information should be displayed on the CheckOut page. Now, click the Cancel Order button to return to the Order page. Then, click the Go to Cart button to see that there isn’t anything in the cart, and click the Check Out button to see that no customer information is displayed. If you encounter any problems, fix them.

# Exercise 3-3 Add images and formatting to the Shopping Cart application

In this exercise, you’ll add images to the Shopping Cart application that you developed in exercises 3-1 and 3-2. That will give you a chance to work with a more complicated table and to format the text in that table.

# Add images to the application

+   1. Add a folder named Images to your web site. Then, add the file named banner.jpg to this folder. You can find this file in the C:\aspnet4_cs\Ch01Cart\Images directory.
+   2. Within the Images folder, add a subfolder named Products. Then, add the jpg files for the products to this subfolder. You can find these files in the C:\aspnet4_cs\Ch01Cart\Images\Products directory.
+   3. Add the banner.jpg file to the top of all the pages in the Shopping Cart application.

# Modify the Order page so it displays the images

+   4. Add a table and formatting to the Order page so it looks similar to the Order page shown in figure 3-1, but without the Quantity text box.
+   5. Add an Image control to the right column of the table, and set the ID property to imgProduct. Also, set the valign property of the cell that contains the image to “top”.
+   6. Add code to the Order page to display the image for the selected product in the Image control. To do that, you can set the ImageUrl property of the Image control to the location of the image file relative to the page appended with the ImageFile property of the Product object for the selected product. Note that this works because the ImageFile property contains a string with the name of the image file.
+   7. Run the application and test the Order page. When it loads, it should display an image for the product that’s selected in the drop-down list. When you select a new product, it should display that product in the Image control.