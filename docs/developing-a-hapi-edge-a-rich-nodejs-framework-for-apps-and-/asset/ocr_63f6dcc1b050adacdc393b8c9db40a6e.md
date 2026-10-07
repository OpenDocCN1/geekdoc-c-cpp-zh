# CHAPTER 2: Server

```
,
options: {
  files: {
    redirectTo: __dirname
  }
};
```

```
exports.init = function (callback) {
  var server = new Hapi.Server();
  server.connection(internals.servers.http);
  server.connection(internals.servers.api);
  //...
};
```

We begin by loading our libraries that we're going to. We've organized our code as Models, Routers, and Controllers. We also have code specifically for our API.
What's new here are the labels. They serve as an indicator for the system that can be used to decide which plugins listen for each connection later. We are likely to have only some plugins listen to one connection and not the other. Some may listen to both, such as a /heartbeat type call, but in general unless one is using SSL/TLS and the other encrypted, there should be little duplication. You can read more about how to select plugins and how to manage plugins in Chapter 6. This is done using the server.register().

```
server.path(internals.options.files.redirectTo);
server.on('request-error', function (request, response) {
  console.log('request-error:');
  console.dir(response);
});
```

server.path indicates to have a path prefix so we can use relative paths to locate files and templates.
We also set an event for handling errors that happen on requests.

```
var registerHttpPlugins = function (next) {
  server.register([
    Bell,
    Blipp,
    HapiAuthCookie,
    Authentication,
```