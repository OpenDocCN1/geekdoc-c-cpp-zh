template that tries to hide it bombs out, and the rest of the template never gets run. As a result, you never see the cart update in the sidebar.

The solution is a little hack. We want to run the .hide only if the notice <div> is present, but RJS doesn’t give us the ability to generate JavaScript that tests for <div>s. It does, however, let us iterate over elements on the page that match a certain CSS selector pattern. So let’s iterate over all <div> tags with an id of notice. The loop will find either one, which we can hide, or none, in which case the hide won’t get called.

```
Download depot_p/app/views/store/add_to_cart.js.rjs
page.select("div#notice").each { |div| div.hide }

page.replace_html("cart", :partial => "cart", :object => @cart)

page[:cart].visual_effect :blind_down if @cart.total_items == 1

page[:current_item].visual_effect :highlight,
  :startcolor => "#88ff88",
  :endcolor => "#114411"
```

The customer likes it. We’ve implemented product maintenance, a basic catalog, and a shopping cart, and now we have a simple ordering system. Obviously we’ll also have to write some kind of fulfillment application, but that can wait for a new iteration. (And that iteration is one that we’ll skip in this book; it doesn’t have much new to say about Rails.)

# What We Just Did

In a fairly short amount of time, we did the following:

+   - We added orders and line_items tables (with the corresponding models) and linked them together.
+   - We created a form to capture details for the order and linked it to the order model.
+   - We added validation and used helper methods to display errors to the user.

# Playtime

Here’s some stuff to try on your own:

+   - Trace the flow through the methods save_order, add_line_items_from_cart, and from_cart_item. Do the controller, order model, and line item model seem suitably decoupled from each other? (One way to tell is to look at potential changes—if you change something, such as by adding a new