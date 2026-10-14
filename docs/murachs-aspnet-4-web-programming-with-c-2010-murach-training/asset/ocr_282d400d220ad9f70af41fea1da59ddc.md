# How security is used by the Halloween Store application

Cart.aspx

CheckOut1.aspx

Secure

CheckOut2.aspx

Order.aspx

Confirmation.aspx

Unsecure

# Description

+   - When the user clicks the Check Out button from the Cart page (or the Order page), the browser is redirected to the first Check Out page using a secure connection.
+   - When the user clicks the Continue Checkout button from the first Check Out page, the browser is redirected to the second Check Out page and remains in the secure connection.
+   - When the user clicks the Accept Order button from the second Check Out page, the browser is redirected to the Confirmation page and remains in the secure connection.
+   - When the user clicks the Return to Order Page button from the Confirmation page, the browser is redirected to the Order page in an unsecured connection.

Figure 18-8   The operation of the Halloween Store application with SSL