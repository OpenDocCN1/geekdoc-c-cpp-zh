And here's the corresponding updates to the locales files:

```
Download depot_s/config/locales/en.yml

en:
  main:
    title: "Your Pragmatic Catalog"
    button:
      add: "Add to Cart"
```

```
Download depot_s/config/locales/es.yml

es:
  main:
    title: "Su Cat&aacute;logo de Pragmatic"
    button:
      add: "A&ntilde;adir al Carrito"
```

Note that since we did not use the Rails h helper function in our ERb template, we are free to use HTML entity names for characters that do not appear on our keyboard:

![](bbox=[0.18, 0.42, 0.85, 0.83])

Feeling confident, we move onto the cart partial:

```
Download depot_s/app/views/store/_cart.html.erb

<div class="cart-title"><%= I18n.t 'layout.cart.title' %></div>
<table>
  <%= render(:partial => "cart_item", :collection => cart.items) %>
```