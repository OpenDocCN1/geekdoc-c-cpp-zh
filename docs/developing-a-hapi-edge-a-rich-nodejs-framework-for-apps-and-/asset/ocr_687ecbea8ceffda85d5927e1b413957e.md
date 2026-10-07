```
cassandraOptions.options
);
client.connect(function (err) {
  if (err) {
    throw err;
  }
  // client is now connected
});
```

```
var Apollo = require('apollo');
exports.register = function (plugin, cassandraOptions, next) {
  var client = new Apollo(cassandraOptions.connection, cassandraOptions.options);
  client.connect(function (err) {
    if (err) {
      throw err;
    }
    plugins.expose('cassandraClient', client);
    next();
  });
```

# POSTGRES:PG

```
var pgOptions = {
  'connection': 'postgres://username:password@localhost/data-base',
  'options': {}
};
```

```
var Pg = require('pg');
var client = new Pg.Client(pgOptions.connection);
client.connect(function (err) {
  if (err) {
    throw err;
  }
  // client is now connected
});
```