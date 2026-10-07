and even have different options settings per environment. This allows you to again keep
things all in one location so things are easier to manage.

# A word on labels and selecting plugins

During registration, plugins can be loaded on specifically designated connections for the
server. This is a really important feature of happi. It allows for the handling of multiple dis-
tinct servers as part of one package. The api can be separated from the logic of presenting
templates this way.

Actually debugging the setup and making the right plugins are registered on the
correct server can be a bit of a challenge. We recommend the blipp plugin in order to see
what's going on in the routing table when loading the server.

```
server.register({
  // plugins
}, { select: 'http' },
function (err) {
  if (err) {
    console.log('server.register err:', err);
  }
  server.register({
    // plugins
  }, { select: 'api' },
  function (err) {
    if (err) {
      console.log('server.register err:', err);
    }
    server.start(function () {
      console.log('server started on port: ', server.info.port);
      return callback(null, server);
    });
  });
});

```

# When to use a plugin

The goal was to better manage your code -- EH