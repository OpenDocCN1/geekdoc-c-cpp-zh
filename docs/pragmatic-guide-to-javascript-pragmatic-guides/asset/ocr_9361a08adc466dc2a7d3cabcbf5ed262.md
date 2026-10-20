# Implement JSON-P with bare-bones code.

In its simplest form, it just goes like this:

```
document.documentElement.firstChild.appendChild(
  new Element('script', { type: 'text/javascript',
    src: this.href + '&r=' + Math.random() }));
```

The previous code executes in the context of a link click handler, so **this** is the `<a>` element being activated.

The random parameter is there to circumvent browser caching; in production code, you’d check the URI to decide whether to prefix it with & or ?.

A more advanced way is to use dynamic id= attributes for such scripts and remove them post-load to avoid flooding the DOM. The dynamic id= can double as random parameter:

```
var script = new Element('script', { type: 'text/javascript',
  src: this.href });
script.src += '&r=' + script.identify();
script.observe('load', Element.remove.curry(script));
document.documentElement.firstChild.appendChild(script);
```

# Use JSON-P facilities from frameworks.

A few frameworks provide functions, specific to JSON-P, that can always come in handy:

```
// jQuery
$.getJSON(url[, data][, callback])
// Mootools
new Request.JSONP({ url: ..., onComplete: function(data) {...} })
// Dojo
dojo.io.script.get({ url: ..., jsonp: function(data) {...} })
```

# Related Tasks

+   - Task 29, *Using JSON*, on page 82
+   - Task 32, *Cross-Domain “Ajax” (Take 2)*, on page 88