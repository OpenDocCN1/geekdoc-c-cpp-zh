# # Make a simple Ajax request.

```
```
// Prototype
new Ajax.Request(url[, options])
new Ajax.Updater(container, url[, options])
// jQuery
$.ajax([settings])
// MooTools
new Request([options])
// YUI < 3
YUI.util.Connect.asyncRequest(method, url, callback, postData)
// YUI >= 3
Y.io(url[, config])
// Dojo
dojo.xhrGet(settings) // or xhrPost, xhrPut, xhrDelete.
// ExtJS
Ext.Ajax.request(settings)
```
```

# # Use more involved, Prototype-based features, for a taste.

```
```
Ajax.Responders.register({
  onCreate: function() { $('spinner').show(); },
  onComplete: function() {
    if (0 == Ajax.activeRequestCount)
      $('spinner').hide();
  }
});

new Ajax.Updater({ success: 'latestUsers' }, '/users/latest', {
  method: 'get',
  parameters: { mode: 'summary', threshold: 'auto' },
  evalScripts: true,
  onFailure: function() {
    logError("We could not fetch the latest logged-in users, sorry.");
  }
});
```
```