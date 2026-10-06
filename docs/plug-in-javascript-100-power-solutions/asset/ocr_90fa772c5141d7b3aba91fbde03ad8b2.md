# Plug-In JavaScript: 100 Solutions

# How It Works

This is a simple function that runs on the fact that all arguments sent to a function can be accessed via the arguments array. What it does is piece all the arguments it sent back to reconstruct an e-mail address using a for() loop, like this:

```
var a = '';
for (var j=0; j < arguments.length; ++j)
  a += arguments[j]
```

The variable is then used to create a hyperlink to the e-mail address, with the code itself using segmented strings to further obfuscate matters. The result is then returned, like this:

```
return "<a href " + "ef" + "=mai" + "lt" + "o:" + a + ">" + a + "</a>";
```

# How To Use It

To use this, break your e-mail address into multiple strings and pass them all to the plug-in. Here's an example showing how to do this for the e-mail address sim@myserver.com.

```
<h2>Please contact me at: <span id='email'></span></h2>
```

```
<script>
window.onload = function() {
  Html('email', ProtectEmail('sim', '.on.j', 'ones', '@myserv', '.er.c', 'om'))
}
</script>
```

Where you wish the e-mail address to be shown, just place an empty span and give it an ID. You can then insert the email address into the innerHTML property of the span from within a section of JavaScript. If you ensure the e-mail address is completely broken into parts, it is doubtful that any known automated harvester will be able to extract it for spamming purposes.

# The Plug-in

```
function ProtectEmail() {
  var a = '';
  for (var j=0; j < arguments.length; ++j)
    a += arguments[j];
  return "<a href " + "ef" + "=mai" + "lt" + "o:" + a + ">" + a + "</a>";
}
```