![](bbox=[0.181, 0.069, 0.842, 0.403])

Figure 10.2: Our checkout screen

We also validate that the payment type is one of the accepted values.[^4][^5]

```
```ruby
class Order < ActiveRecord::Base
  PAYMENT_TYPES = [
    # Displayed          stored in db
    [ "Check",           "check" ],
    [ "Credit card",     "cc" ],
    [ "Purchase order",  "po" ]
  ]

  validates_presence_of :name, :address, :email, :pay_type
  validates_inclusion_of :pay_type, :in =>
    PAYMENT_TYPES.map {|disp, value| value}

  # ...
```
```

Note that we already call the error_messages_for helper at the top of the page.

> [^4]: To get the list of valid payment types, we take our array of arrays and use the Ruby map method to extract just the values.
> 
> [^5]: Some folks might be wondering why we bother to validate the payment type, given that its value comes from a drop-down list that contains only valid values. We do it because an application can't assume that it's being fed values from the forms it creates. Nothing is stopping a malicious user from submitting form data directly to the application, bypassing our form. If the user set an unknown payment type, they might conceivably get our products for free.