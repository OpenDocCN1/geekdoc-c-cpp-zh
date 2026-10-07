# SOLUTION

Modern browsers now support a system called Content Security Policy. By returning a bunch of HTTP headers, it is possible to force the browser to create a whitelist of acceptable domains and restrict script-scrl calls to this list.
Use Blankie in combination with scooter to quickly define CSP rules.

```
var Hapi = require('hapi');
var Blankie = require('blankie');
var Scooter = require('scooter');

var server = new Hapi.Server();

server.pack.register([Scooter, {
plugin: Blankie,
options: {} // specify options here
}], function (err) {

if (err) {
  throw err;
}

server.start();
});
```

# CORS

By default, a modern browser will prevent AJAX calls to any domain that does not match the current page's domain. This is because major web browsers enforce a “Same-Origin” policy. This Same-Origin policy is a critical aspect of web security.
However, as a developer, you might want to allow your web application to directly access a third-party API, or your own API but on a different domain.
CORS, Cross-Origin Resource Sharing, allows you to do this in a safe and secure manner by explicitly specifying which domains the browser is allowed to connect to via AJAX. This is done by sending custom headers to the browser on response.

# SOLUTION

hapi supports CORS out of the box, but it is disabled by default for security. Enabling it is as simple as setting the ‘cors’ server option to true or passing it a configuration object with one or more allowed ‘origins’.

```
var serverOptions = {
  // ...
  cors: {
```