All of the common options we covered earlier are available for link_to_remote.
Look at this more detailed example:

```
<div id="inbox_status">Unknown</div>
<%= link_to_remote 'Check Status...',
    :url => {:action => 'get_inbox_status',
             :user_id => @user.id},
    :update => 'inbox_status',
    :condition => "$('inbox_status').innerHTML == 'Unknown'",
    :before => "Element.show('progress_indicator')",
    :complete => "Element.hide('progress_indicator')" %>
```

This version will fire the XHR request only if the current value of the target element is “Unknown”, thus preventing the user from requesting the data twice. It uses the :before and :complete options to turn on and off progress indication.

# periodically_call_remote

Instead of relying on the user to make the remote call, you might want to call the server at regular intervals to check for changes. For example, in a web-based chat application, you would want to ask the server every few seconds whether a new chat message had arrived. This is a common way to supply distributed status checking and is a stand-in for a real “push” communication technology.

The periodically_call_remote method takes care of this for you. It works almost exactly like link_to_remote, except instead of taking a string value to use as the link text, it takes an interval value that tells it how long to go between posts to the server. Let’s modify the previous example to show the user’s inbox status every sixty seconds:

```
<div id="inbox_status">Unknown</div>
<%= periodically_call_remote :url => {:action => 'get_inbox_status',
                                 :user_id => @user.id},
    :update => 'inbox_status',
    :frequency => 60,
    :condition => "$('inbox_status').innerHTML == 'Unknown'",
    :before => "Element.show('progress_indicator')",
    :complete => "Element.hide('progress_indicator')" %>
```

periodically_call_remote takes the same options as link_to_remote (as well as the option :frequency). This means that you could provide a value for the :confirm option. Be very careful here. Not only will a modal dialog box pop up asking the user to approve an otherwise completely transparent event, but while the dialog box is onscreen, the timer managing periodically_call_remote is still ticking and firing off the confirmation requests. This means that you could easily get in a situation where the confirmation dialog boxes are piling up and every time you click OK or Cancel the dialog box disappears only to be immediately replaced with another.