fragment component of the URL using the window.location.hash property. The value of this property can easily be manipulated by attackers, and we should treat this data as untrusted.

```
// Source
const untrustedData = window.location.hash;
```

Next, we are passing this untrusted data directly to document.write and document.writeln methods. These methods write a string directly to the document stream as it is being rendered by the browser. The argument passed to both methods is treated as HTML markup. If the markup passed by the attacker contains a script tag with malicious JavaScript code in it, that code will be executed by the browser.

```
// Sinks
document.write(untrustedData);
document.writeln(untrustedData);
```

This way, document.write can become an execution sink. Direct calls to document.write that attackers can leverage are relatively rare in applications. It is much more common for developers to use the DOM API to manipulate structure and content of the page. In this example, we will use the document.getElementById method to obtain a reference to a div node with the identifier, container.

```
const div = document.getElementById("container");
```

Similar to document.write, some methods and properties of the DOM API will treat the parameters passed in as HTML markup and will