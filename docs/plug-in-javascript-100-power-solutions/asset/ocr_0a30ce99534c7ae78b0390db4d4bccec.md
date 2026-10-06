# 334 Plug-In JavaScript: 100 Power Solutions

If the object creation was successful, it goes on open up the request, passing a type of 'POST' in POST, the URL in URL, and the value true, for an asynchronous request:

```
ajax.open('POST', url, true)
```

Next, the content type, and connection headers are sent:

```
ajax.setRequestHeader('Content-type', contenttype)
ajax.setRequestHeader('Content-length', args.length)
ajax.setRequestHeader('Connection', 'close')
```

Finally, the request is sent and the value true is returned to indicate success:

```
ajax.send(args)
return true
```

# How To Use It

You call the plug-in exactly the same way as GetAjaxRequest()—it's just that the process used by the plug-in to perform the Ajax is a POST, not a GET request. Therefore, the target of the request also needs to respond to the POST request, as is the case with the following example, which fetches the details at Anchorage, Alaska airport:

```
<div id=''></div>
```

```
<script>
window.onload = function() {
  url = 'ajaxpost.php'
  args = 'http://www.weather.com/xml/current_obs/PANC.rss'
  PostAjaxRequest('a', todiv, url, args)
}
function todiv() {
  var rss = this.replace(/</g, '&lt;');
  rss = rss.replace(//>/g, '&gt;');
  rss = rss.replace(/\n/g, '<br />');
  Html('a', rss)
}
</script>
```

The URL used to the plug-in is in the PHP script ajaxpost.php. It's another one-line PHP script, which looks like this:

```
<?php if (isset($_POST['url'])) echo file_get_contents($_POST['url']); ?>
```

This is almost same as the ajaxget.php script that it processes POST requests. You can copy it to your own server, where it should work if it supports PHP.

This example is a little more interesting than the previous two in an RSS feed fetched. It's no different than a web page as for Ajax is concerned, but displaying after