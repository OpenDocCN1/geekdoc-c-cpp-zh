# Liking a plugin example

As a large example, we're going to take a look at what is happening behind the scenes when we use a plugin on the site. Below is the example.

```
module.exports.like = {
  auth: 'session',
  handler: function (request, reply) {
    var pluginName = request.params.name;
    var username = request.auth.credentials.username;

    if (!username) {
      return reply (Boom.unauthorized);
    }

    var getPlugin = function (user, next) {
      DB.plugin.get(pluginName, function (err, plugin) {
        if (err || !plugin) {
          var msg = 'no such plugin found';
          return next (Boom.notFound(msg));
        }
        return next (null, plugin, user);
      });
    };

    var addLike = function (plugin, user, next) {
      user.like(plugin, function (err) {
        return next (err);
      });
    };

    Async.waterfall([
      getOrCreateUser,
      getPlugin,
      addLike
    ], function (err, result) {
      if (err) {
        return reply(err);
      }
      return reply({success: true});
    });
  }
};
```