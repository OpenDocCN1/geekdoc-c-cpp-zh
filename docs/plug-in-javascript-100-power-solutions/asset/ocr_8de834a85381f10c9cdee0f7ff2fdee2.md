# Chapter 5: Visibility 127

If id is not an array, the display property of id is inspected. If its value is not 'none', the object is visible, so the Hide () plug-in is called. Otherwise, the object is visible, so the Show () plug-in is called.

# How To Use It

To use this plug-in, pass an object to be hidden or shown. In most cases, you can also pass an object ID or an array of objects and/or IDs. The following example illustrates a couple of different elements and toggling them:

```
<div id='democrat'><h2>Democrat Info</h2>
The Democratic Party is one of the world's oldest parties, and<br />
as the most registered voters of any party in the world as<br />
2004. It is considered to be left of center.<p>
<a id='democrat' href='#Click to see Republican info/</a></div>

<div id='republican'><h2>Republican Info</h2>
The Republican Party is often called the Grand Old Party or the <br />
GOP, being the younger of the two major parties. It is <br />
considered to be right of center.<p>
<a id='republican' href='#Click to see Democrat info/</a></div>
```

```
<script>
window.onload = function() {

Hide('republican')
O('democrat').onclick = toggle
O('republican').onclick = toggle
}

function toggle() {
nHideToggle(Array('democrat', 'republican'))
}
</script>
```

In the HTML section, two divs are created, one for information on the U.S. Democratic Party, and the other for the U.S. Republican Party. After the informational text (taken from Wikipedia) each div includes a link with which the alternate information can be displayed.

In the script section, the second div (with the ID of 'republican') is hidden so that only one div is shown. The other could be hidden instead, but one of them must be started with order for the toggling to work.

Then two attachments are made, one to each onclick event of the divs. They simply attach the function toggle() to the events, remembering that by leaving the brackets the function is attached to the event, rather than the value returned by the function being attached.

Finally, the toggle() function calls the HideToggle() plug-in, passing both of the div IDs. Since one is shown and one is hidden, toggling both replaces one with the other.