# link_to_function

Although not technically a Prototype helper, link_to_function is a commonly used Ajax-enabling helper from the standard Rails helper libraries. It lets you provide the link text and a snippet of JavaScript to execute when the link is clicked. It does not accept all the fancy options we looked at earlier; instead, you can pass any of the various HTML options accepted by the more standard link_to helper.

link_to_function lets you create arbitrary links to invoke client-side functions. The JavaScript need not be relegated to client-side activity only, though. You can provide a JavaScript snippet that invokes XHR as well. This helper (and its act-a-like cousin button_to_function) is for creating more customized interaction models than can be expressed through the common Prototype helpers and options.

For example, you may be using the excellent Prototype Window Class framework by Sébastien Gruhier (http://prototype-window.xilinus.com/). Built on top of Prototype and Script.aculo.us, this framework lets you create JavaScript-only windows inside your application. You might want to create a link that launches a Prototype window to display the About information for your application:

```
<%= link_to_function "About...",
  "Dialog.alert({url: 'about.html', options: {method: 'get'}},
  {windowParameters: {className: 'default'}, 
okLabel: 'Close'});" %>
```

# remote_function

It turns out that the Prototype helpers described previously all use another Prototype helper, remote_function, to actually generate the XHR call. You can use this helper yourself if you want to embed XHR calls in other contexts besides links and periodical executors.

Let’s say that your users have checked the status of their inbox and want to look at the messages. A standard interface might be to display a list of message subjects and then allow the user to select one to view. However, you know your users are used to thick-client mail interfaces, and the standard interaction is to double-click the e-mail subject to view the message. You want to provide the same functionality, but you need to make an XHR call to the server to fetch the specific e-mail. This example is the partial you might use to render the list:

```
<table>
  <% for email in @emails %>
  <tr ondblclick="<%= remote_function(:update => 'email_body',
                                    :url => {:action => 'get_email',
                                    :id => email}) %>">
    <td><%= email.id %></td><td><%= email.body %></td>
  </tr>
  <% end %>
</table>
<div id="email_body"></div>
```