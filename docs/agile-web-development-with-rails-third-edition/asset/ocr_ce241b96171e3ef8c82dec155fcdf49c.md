```
def mark_as_paid
  @order = Order.find(params[:id])
  @order.mark_as_paid
  @order.save
end
end
```

OK, so it's not great code, but it illustrates a problem. Clearly, the accept_order method is intended to handle a POST request from a form. The developer decided to factor out its two responsibilities by wrapping them in two separate controller methods, process_payment and mark_as_paid.

Unfortunately, the developer left these two helper methods with public visibility. This means that anyone can enter the following in their browser:

http://unlucky.company/order/mark_as_paid/123

and order 123 will magically be marked as being paid, bypassing all credit-card processing. Every day is free giveaway day at Unlucky Company.

The basic rule is simple: the only public methods in a controller should be actions that can be invoked from a browser.

This rule also applies to methods you add to application.rb. This is the parent of all controller classes, and its public methods can also be called as actions.

# 27.5 Cross-Site Scripting (CSS/XSS)

Many web applications use session cookies to track the requests of a user. The cookie is used to identify the request and connect it to the session data (session in Rails). Often this session data contains a reference to the user that is currently logged in.

Cross-site scripting is a technique for “stealing” the cookie from another visitor of the website and thus potentially stealing that person’s login.

The cookie protocol has a small amount of built-in security; browsers send cookies only to the domain where they were originally created. But this security can be bypassed. The easiest way to get access to someone else’s cookie is to place a specially crafted piece of JavaScript code on the website; the script can read the cookie of a visitor and send it to the attacker (for example, by transmitting the data as a URL parameter to another website).

# A Typical Attack

Any site that displays data that came from outside the application is vulnerable to XSS attack unless the application takes care to filter that data. Sometimes the path taken by the attack is complex and subtle. For example, consider a shopping application that allows users to leave comments for the