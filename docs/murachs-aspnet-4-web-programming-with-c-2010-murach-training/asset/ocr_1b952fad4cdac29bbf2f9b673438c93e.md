# Exercise 1-2 Use your web browser to run the Shopping Cart application on your PC

In this exercise, you’ll use your web browser to run the Shopping Cart application that’s illustrated in this chapter. This assumes that you’ve already installed IIS, Visual Studio 2010, and the files for these exercises as described in appendix A. When you get this application running, you’ll know that you’ve got IIS and the application set up correctly on your PC. Note that if you’re using Windows XP Home Edition, Windows Vista Home Basic or Starter Edition, or Windows 7 Home Basic or Starter Edition, you won’t be able to do this exercise. That’s because these editions don’t come with IIS, or the version of IIS they come with doesn’t support ASP.NET development.

# Create a virtual directory for the Shopping Cart application

+   If you’re using Windows 7 or Windows Vista, use the procedure in figure B-1 of appendix B to create an IIS application named Ch01Cart under the Default Web Site node for the application in C:\aspnet4_cs\Ch01Cart. If you’re using Windows XP, use the procedure in figure C-1 of appendix C to create an IIS virtual directory named Ch01Cart under the Default Web Site node for the application in C:\aspnet4_cs\Ch01Cart.

# Run the Shopping Cart application

+   Open your web browser, and type in the following URL, which uses the virtual directory as the path:

http://localhost/Ch01Cart/Order.aspx

This should start the Shopping Cart application that’s shown in figure 1-1. If it doesn’t, make sure that IIS is installed and running, that the exercise files are installed, and that you did step 1 correctly.

+   Select a product from the drop-down list on the Order page that’s displayed. Note that this starts a postback that returns the Order page with the data and image for the product that was selected.

+   Enter a quantity and click the Add to Cart button to display the Cart page. Then, click the Continue Shopping button to return to the Order page.

+   Continue to experiment with this application until you understand how it works. Note that because this application doesn’t include data validation, you’ll get an error if you click the Add to Cart button on the Order page without entering a quantity. When you’re done, click the Close button in the upper right corner of the browser window to end the application.