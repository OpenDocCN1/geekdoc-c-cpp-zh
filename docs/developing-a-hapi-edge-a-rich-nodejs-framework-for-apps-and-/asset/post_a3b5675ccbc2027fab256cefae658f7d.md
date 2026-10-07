
plugin.bind is used when we want to be able to access some piece of data throughout the application but we don't want to keep loading it. This can be initializing or reinstating some piece of data and we only need to do it one time, perhaps setting up a session, or something else specific to the whole lifecycle of the app.
Our lib/routes.js has examples of both use-cases.

```javascript
plugin.dependency('controllers');
plugin.dependency('models');
var Controllers = plugin.plugins.controllers.handlers;
var Models = plugin.plugins.models.models;
plugin.bind({
  models: Models
});
```

The routes require the controllers to be set up first since they contain the handlers that uses routes. The models will be used in the routes route. In addition, because of the bind, the database models will now be accessible anywhere in the handlers as simple this.models.

# Plugin configuration

Previously, you may not have noticed that there was an arguments that was passed when registering a plugin via the register function. To show you again:

```javascript
exports.register = function (plugin, options, next) {
  load({path: __dirname + '/handlers'}, function (err, handlers) {
    if (err) {
      throw err;
    }
    if (process.env.DEV) {
      console.log('handlers:');
    }
    plugin.expose('handlers', handlers);
    next();
  });
}
```

You can see that options wasn't used anywhere. However, options can be used to configure the plugin. Let's suppose we wanted to pass some options for the blipp plugin. Recall this plugin just lists the routes on startup. While routes don't currently support this,

# CHAPTER 6: Plugins

it's conceivable that you wouldn't blipp to actually print the routes table in colors on startup, so you may want to pass it a flag saying to just print without ANSI colors. We should be able to see something like the following instead of our original code:

```javascript
server.register([
  { register: Blipp, options: { colors: false } },
  HapiAuthCookie,
  Authentication,
  Controllers,
  Models,
  Routes
], function (err) {
  if (err) {
    console.log('server.register err:', err);
    return callback(err);
  }

  server.start(function () {
    console.log('server started on port: ', server.info.port);
    return callback(null, server);
  });
});
```

The code above is for our entire server instance. The actual blipp plugin would have a register function that would look like the following:

```javascript
exports.register = function (server, options, next) {
  if (options.color === true) {
    // do colors
  } else {
    // turn off colors
  }
}
```

In our startup, we had options set to { colors: false }. We pass these options to the plugin, and the plugin knows to turn off the colors. We saw options being passed back in Chapter 2. If you look in the rejoice and glue areas, you will see how options for the plugins are being passed to the plugin. An example of this is the opsInterval in the good plugin area. You can configure your options right in confidence

and even have different options settings per environment. This allows you to again keep things all in one location so things are easier to manage.

# A word on labels and selecting plugins

During registration, plugins can be loaded on specifically designated connections for the server. This is a really important feature of happi. It allows for the handling of multiple distinct servers as part of one package. The api can be separated from the logic of presenting templates this way.

Actually debugging the setup and making the right plugins are registered on the correct server can be a bit of a challenge. We recommend the blipp plugin in order to see what's going on in the routing table when loading the server.

```javascript
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

# CHAPTER 6: Plugins

We've already touched on some cases of when to use a plugin, let's go over them again and be more specific. Using plugins correctly can help you architect your code well.
You'll want to create a plugin if there's anything that you can do to separate the work from the rest and reuse across different projects. You may have started looking at the various plugins for a project, and not found one that suits your needs. It's possible to create your own plugin. One of the authors found unlike popular frameworks like Ruby on Rails, there was no way to have hapi list the different routes that were available from the start of the app. A plugin was created just to show some information.

A project may be, as mentioned earlier, also based on the routes available. A plugin may be completely dedicated to serving up the routes for a specific path. We may have all of the routes in the plugin.

```javascript
plugin.route([
  { method: 'GET', path: '/plugins/upload', config: Controllers.Plugin.GetUpload },
  { method: 'POST', path: '/plugins/upload', config: Controllers.Plugin.PostUpload },
  { method: 'GET', path: '/plugins/{name}/download', config: Controllers.Plugin.download }
])
```

And we may have another plugin to handle user information.

```javascript
plugin.route([
  { method: 'GET', path: '/user', config: Controllers.User.get },
  { method: 'PUT', path: '/user/profile', config: Controllers.User.updateProfile }
])
```

This will make more sense if you have a large project and you need to divide the work because routes take a lot of logic.

# The hapi plugin ecosystem: some common plugins

Let's look at some of the popular plugins in the hapi ecosystem. You can find more plugins on hapi-plugins.com (of course) but we've taken the liberty to show some of the major ones.

# hapi-auth-basic

This plugin provides basic authentication for logging into the application, or just basic authentication in general. Most web-based systems require some form of authentication to gain access to the data. Many frameworks as part of the framework, but by using this modular approach, any authentication form is possible.
More information on hapi-auth-basic is provided in Chapter 7.

# blipp

While blipp isn't a core plugin, it's nevertheless very useful. It simply displays the routes and the server:port combination when the hapi server is started. It gives a quick indication of what routes are available and that they're on the correct server connection.

# bell

Bell is much like hapi-auth-basic except that it's using third-party logins such as Facebook, GitHub, Instagram, Twitter, Foursquare, VK, ArcGIS Online and Windows Live. If you're looking for logins for this, this is the plugin to use. Third-party plugins are getting added continually. Bell is usually used with hapi-auth-cookie so that isn't explicitly called out on its own.
More information on bell and hapi-auth-cookie is provided in Chapter 7.

# good

If you're running a service in production, you'd almost certainly want to use good. You get to see how your service is performing with cpu usage, memory, etc. There are many reporters you can use with this program, you can have reports sent to a file logger, to console, or any custom program you write your own reporter for.
More information on good is provided in Chapter 11.

# tv

TV is an interactive module used for debugging. It becomes easy to see what requests are received by your service and what it does to handle it.
More information on tv is provided in Chapter 11.

# lout / hapi-swagger

Lout and hapi-swagger are documentation tools for your routes and setup. It provides api documentation for you, so you don't have to this. This can save you some serious time for something that you need to have anyway.
