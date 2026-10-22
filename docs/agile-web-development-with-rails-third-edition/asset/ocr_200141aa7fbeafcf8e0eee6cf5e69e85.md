```
<tr class="total-line">
    <td colspan="2">Total</td>
    <td class="total-cell"><%= number_to_currency(cart.total_price) %></td>
</tr>

</table>
```

```
<%= button_to I18n.t('layout.cart.button.checkout'), :action => 'checkout' %>
<%= button_to I18n.t('layout.cart.button.empty'), :action => :empty_cart %>
```

Download depot_s/config/locales/en.yml

```
en:
  cart:
    title: "Your Cart"
    button:
      empty: "Empty cart"
      checkout: "Checkout"
```

Download depot_s/config/locales/es.yml

```
es:
  layout:
    cart:
      title: "Carrito de la Compra"
      button:
        empty: "Vaciar Carrito"
        checkout: "Comprar"
```

![](bbox=[0.18, 0.54, 0.85, 0.95])