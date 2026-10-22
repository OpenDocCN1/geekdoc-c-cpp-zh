messages. For example, when our add_to_cart action detects that it was passed an invalid product id, it can store that error message in the flash area and redirect to the index action to redisplay the catalog. The view for the index action can extract the error and display it at the top of the catalog page. The flash information is accessible within the views by using the flash accessor method.

Why couldn’t we just store the error in any old instance variable? Remember that after a redirect is sent by our application to the browser, the browser sends a new request back to our application. By the time we receive that request, our application has moved on—all the instance variables from previous requests are long gone. The flash data is stored in the session in order to make it available between requests.

Armed with all this background about flash data, we can now change our add_to_cart method to intercept bad product ids and report on the problem:

```
Download depot_h/app/controllers/store_controller.rb

def add_to_cart
  product = Product.find(params[:id])
  @cart = find_cart
  @cart.add_product(product)
rescue ActiveRecord::RecordNotFound
  logger.error("Attempt to access invalid product #{params[:id]}")
  flash[:notice] = "Invalid product"
  redirect_to :action => 'index'
end
```

The rescue clause intercepts the exception raised by Product.find. In the handler, we do the following:

+   - Use the Rails logger to record the error. Every controller has a logger attribute. Here we use it to record a message at the error logging level.

+   - Create a flash notice with an explanation. Just as with sessions, you access the flash as if it were a hash. Here we used the key :notice to store our message.

+   - Redirect to the catalog display using the redirect_to method. This takes a wide range of parameters (similar to the link_to method we encountered in the templates). In this case, it instructs the browser to immediately request the URL that will invoke the current controller's index action. Why redirect, rather than just display the catalog here? If we redirect, the user's browser will end up displaying a URL of http://.../store/index, rather than http://.../store/add_to_cart/wibble. We expose less of the application this way. We also prevent the user from retriggering the error by hitting the Reload button.