partial once for each item in the collection. Let’s rewrite our cart view to use this feature:

```
```erb
<div class="cart-title">Your Cart</div>
<table>
  <%= render(:partial => "cart_item", :collection => @cart.items) %>

  <tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(@cart.total_price) %></td>
  </tr>

</table>

<%= button_to "Empty cart", :action => :empty_cart %>
```
```

That’s a lot simpler. The render method takes the name of the partial and the collection object as parameters. The partial template itself is simply another template file (by default in the same directory as the template that invokes it). However, to keep the names of partials distinct from regular templates, Rails automatically prepends an underscore to the partial name when looking for the file. That means our partial will be stored in the file _cart_item.html.erb in the app/views/store directory.

```
```erb
<tr>
  <td><%= cart_item.quantity %>&times;</td>
  <td><%=h cart_item.title %></td>
  <td class="item-price"><%= number_to_currency(cart_item.price) %></td>
</tr>
```
```

There’s something subtle going on here. Inside the partial template, we refer to the current cart item using the variable cart_item. That’s because the render method in the main template arranges to set a variable with the same name as the partial template to the current item each time around the loop. The partial is called cart_item, so inside the partial we expect to have a variable called cart_item.

So, now we’ve tidied up the cart display, but that hasn’t moved it into the sidebar. To do that, let’s revisit our layout. If we had a partial template that could display the cart, we could simply embed a call like this within the sidebar:

```
```ruby
render(:partial => "cart")
```
```

But how would the partial know where to find the cart object? One way would be for it to make an assumption. In the layout, we have access to the @cart instance variable that was set by the controller. It turns out that this is also available inside partials called from the layout. However, this is a bit like calling a method and passing it some value in a global variable. It works, but it’s