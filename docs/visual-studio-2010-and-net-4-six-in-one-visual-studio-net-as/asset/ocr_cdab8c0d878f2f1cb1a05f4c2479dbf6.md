dangerous. On the other hand, it breaks a really painful limit of Web 2.0 applications, so it is not a surprise that the Microsoft Ajax Library fully supports JSON.

In the next example, you will see how you incorporate Twitter into your web page with JSON and the Microsoft Ajax Library. After importing the MicrosoftAjax.js and the MicrosoftAjaxTemplates.js files, create a DataView that displays the Tweets of a user:

```
<ul>
  <li id="Results"
      class="sys-template"
      sys:attach="dv">
  </li>
  <li>
      <b>{{ text }}</b>
      <br />
      {{ created_at }}
  </li>
</ul>
```

Code file [4-ServerSideData\8-JSONP.htm] available for download at Wrox.

You can create an input box and button to ask the user for a Twitter account to query:

```
<input type="text" id="txtName" />
<input type="button" value=getTweets onclick="getTweets();" />
```

Code file [4-ServerSideData\8-JSONP.htm] available for download at Wrox.

When the user clicks on the button, the following getTweets function is called:

```
function getTweets() {
  var userName = $_get('txtName');
  var uri = =
    String.format("http://twitter.com/status/user_timeline/{0}.json?count=5",
    encodeURI(userName));
  Sys.Net.WebServiceProxy.invoke(uri, null, true, null, onComplete);
}
```

Code file [4-ServerSideData\8-JSONP.htm] available for download at Wrox.

In this function, the username is first read from the textbox, then the static method of the WebServiceProxy class is called with the service URI and the third true parameter means that the service should be called with an HTTP GET request.

After the successful service call, the Ajax Library calls the callback function onComplete, in which you can set the result data as the data source of the DataView: