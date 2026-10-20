# Use a CORS-compliant XMLHttpRequest.

Download server/crossdomain1/crossdomain1.js

```
new Ajax.Updater({ success: 'responses' }, this.href, {
  method: 'get', insertion: 'bottom'
});
```

# Use a server-side proxy (from the current domain).

Download server/crossdomain1/crossdomain1.js

```
new Ajax.Updater({ success: 'responses' }, 'ssp.php', {
  method: 'get', parameters: { uri: this.href }, insertion: 'bottom'
});
```

# Use a dynamically generated form and <iframe>.

Download server/crossdomain1/crossdomain1.js

```
var warp = new Element('iframe', { name: '__blackhole' });
warp.setStyle('width: 0; height: 0; border: 0');
document.body.appendChild(warp);
warp.observe('load', function() {
  $('responses').insert('<p>OK, posted.</p>');
});
var form = new Element('form', { method: 'post', action: this.href,
  target: '__blackhole' });
form.submit();
```

# Use a dynamically generated form on a 204 resource.

Download server/crossdomain1/crossdomain1.js

```
var form = new Element('form', { method: 'post', action: this.href });
form.submit();
Element.insert.defer('responses', '<p>OK, posted.</p>');
```

# Related Tasks

+   - Task 32, Cross-Domain "Ajax" (Take 2), on the next page