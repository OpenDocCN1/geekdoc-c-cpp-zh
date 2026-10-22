# Creating the Order Capture Form

Now that we have our tables and our models, we can start the checkout process. First, we need to add a Checkout button to the shopping cart. We'll link it back to a checkout action in our store controller:

```
Download depot_p/app/views/store/cart.html.erb
<div class="cart-title">Your Cart</div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
  </tr>

</table>

►
<%= button_to "Checkout", :action => 'checkout' %>
<%= button_to "Empty cart", :action => :empty_cart %>
```

We want the checkout action to present our user with a form, prompting them to enter the information in the orders table: their name, address, e-mail address, and payment type. This means that at some point we'll display a Rails template containing a form. The input fields on this form will have to link to the corresponding attributes in a Rails model object, so we'll need to create an empty model object in the checkout action to give these fields something to work with.² (We also have to find the current cart, as it is displayed in the layout. Finding the cart at the start of each action is starting to get tedious; we'll see how to remove this duplication later.)

```
Download depot_p/app/controllers/store_controller.rb
def checkout
  @cart = find_cart
  if @cart.items.empty?
    redirect_to_index("Your cart is empty")
  else
    @order = Order.new
  end
end
```

Notice how we check to make sure that there's something in the cart. This prevents people from navigating directly to the checkout option and creating empty orders.

Now for the template itself. To capture the user's information, we'll use a form. As always with HTML forms, the trick is populating any initial values into the

> 2. Again, if you're following along, remember that actions must appear before the private keyword in the controller.