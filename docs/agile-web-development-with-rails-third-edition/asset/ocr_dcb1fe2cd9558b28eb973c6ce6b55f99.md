When a headers ‘return-path’ is specified, that value will be used as the “envelope from” address. Setting this is useful when you want delivery notifications sent to a different address from the one in from.

```
headers "Organization" => "Pragmatic Programmers, LLC"
```

recipients array or string
One or more recipient e-mail addresses. These may be simple addresses, such as dave@pragprog.com, or some identifying phrase followed by the e-mail address in angle brackets.

```
recipients [ "andy@pragprog.com", "Dave Thomas <dave@pragprog.com>" ]
```

reply_to array or string
These addresses will by listed as the default recipients when replying to your email. Sets the e-mail's Reply-To: header.

sent_on time
A Time object that sets the e-mail's Date: header. If not specified, the current date and time will be used.

subject string
The subject line for the e-mail.

The body takes a hash, used to pass values to the template that contains the e-mail. We'll see how that works shortly.

# E-mail Templates

The generate script created two e-mail templates in app/views/order_mailer, one for each action in the OrderMailer class. These are regular .erb files. We'll use them to create plain-text e-mails (we'll see later how to create HTML e-mail). As with the templates we use to create our application's web pages, the files contain a combination of static text and dynamic content. We can customize the template in confirm.erb; this is the e-mail that is sent to confirm an order:

```
Download e1/mailer/app/views/order_mailer/confirm.erb
```

```
Dear <%= @order.name %>

Thank you for your recent order from The Pragmatic Store.

You ordered the following items:

<%= render(:partial => "/line_item", :collection => @order.line_items) %>

We'll send you a separate e-mail when your order ships.
```

There's one small wrinkle in this template. We have to give render the explicit path to the template (the leading ./) because we're not invoking the view from a real controller and Rails can't guess the default location.