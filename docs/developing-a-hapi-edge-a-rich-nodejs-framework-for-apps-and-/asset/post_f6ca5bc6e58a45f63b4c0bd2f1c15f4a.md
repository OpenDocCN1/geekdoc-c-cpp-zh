
# CHAPTER 8: Models

```
}
);
```

Now you have seen two ways to create Models that make calls to RESTful API endpoints. One was a general way to make requests and the second was to generate happy wrappers to make requests. It is fairly easy to adapt any of these examples to accommodate other third-party RESTful APIs in your projects.

Next up, we'll continue exploring models and how to connect and query a database.

# Using a database

In general, developers have complete flexibility when using databases hapi - any database, any ORM, or any library can be used. You can use one database for one project, another for a second project, or use ten databases for a third project. hapi tries to make developers happy by not getting in the way.

For the github.com/hapi-edge/hapi-plugins application, we've selected the popular MongoDB for our database and we will use the Mongoose driver to connect to our database. For information about other database options and why we choose MongoDB, please see the Models section of Chapter 13 Appendix.

# Setting up the database

Setting MongoDB for an application is fairly well documented on mongodb.org. However, for rapid development, it is faster to develop locally or to Compose (aka MongoHQ) to generate a free database instance for you.

Once an instance is set up, a database name needs to be created. We have chosen the instance name 'hapi-plugins' and a database name 'hapi-plugins'. If you change these names, remember to replace them in the examples below in the connection string. If you set up authentication using a username and password (like how we setup in our production database), remember to add that to the connection string.

Collections are lists of documents. Mongoose will create these for you as you use so it is not necessary to create by hand unless you want to impose size and maximum document limits.

# Connecting to the database

Mongoose provides a high level API for connecting the MongoDB instance. It accepts only a mongodb connection string that can contain host, username, password, database, and so on. Subsequent calls and queries to the database are automatically queued until the connection is complete. Therefore, it is not necessary to nest code in an asynchronous block while waiting for the connection to be made.

In the hapi-plugins.com application, we want to connect to a locally running instance of MongoDB while we develop, but then we also want to connect to the production database when deployed. We use environment variables dictate what environment to run. The Node.js global, process-wide variable process.env contains all of the environment variables available to our application.

To enable production, we run our application as PRODUCTION=1 node index.js.

Note: Database credentials in this chapter have their passwords removed. Replace these credentials with proper ones for the database that you created.

```
var databases = {
  development: 'mongodb://localhost/hapi_plugins',
  production: 'mongodb://hapi:({PASSWORD})@c278.lighthouse.0.mongodbayer.com:10278,c278.lighthouse.1.mongodbayer.com:10278/hapi-plugins?replicaSet=set-54ebe6966d607dala000f09'
};
```

```
if (process.env.PRODUCTION) {
  Mongoose.connect(databases.production);
} else {
  Mongoose.connect(databases.development);
}
```

Using this pattern, we can easily differentiate the environments. When developing locally, we use a local database. Then, production uses the live, scalable, hosted database. An alternative pattern is to include the database connection string itself in the ENV like so:

```
// MONGO_STR='mongodb://localhost/hapi_plugins' node index.js
Mongoose.connect(process.env.MONGGO_STR);
```

This has added benefit of not storing your connection string anywhere in your code. This may be extremely important if you plan to open your source code or in the event your application servers become compromised, hackers would have direct access to your database after reading the code.

# Schema Design

Before we make any queries to the database, it is generally helpful to design a rough schema beforehand. Even though MongoDB does not require or enforce Schemas, as schemas define how your data is structured and can help you enforce data types. It helps to know how you plan to access and use the data first.

For the hapi-plugins.com application, we plan to allow anonymous visitors to:

- Search for plugins by name, description, author, and keyword.
- Log in & manage your plugins
- Add your own plugin to the list
- Like or unlike a plugin

In the background, we also need to be able to:

- Add a plugin to the list
- Remove a plugin from the list

Therefore, we know plugins must have a name, description, author(s), and keywords. NPM prevents duplicate module names, so we know that names will be unique and thus we can use name as a primary key. Also, we from looking at NPM modules also have versions, licenses, repository URLs, homepages, dependencies, dependents, and a bunch of statistics. It also has time information about how the module was created and updated. From this, we can define our first schema for our hapi-plugins app.

```
var internals = {};

internals.plugin = new Mongoose.Schema({
  'name': { type: String, required: true },
  'description': { type: String, required: false },
  'version': { type: String, required: true },
  'authors': { type: Array, required: false },
  'license': { type: String, required: false },
  'repository': { type: String },
  'homepage': { type: String },
  'updated_at': { type: Date, default: Date.now },
  'created_at': { type: Date, default: Date.now },
  'keywords': { type: Array },
  'dependencies': { type: Array },
  'dependents': { type: Array },
  'stats': {
    'releases': { type: String },
    'downloads': { type: String },
    'downloads_this_month': { type: String },
    'open_issues': { type: String },
    'pull_requests': { type: String }
  }
});
var plugin = Mongoose.model('plugin', internals.plugin);
```

# Using a database

In the above schema, we have defined all of the relevant fields in each document and some data type requirements. In some cases, there are also defaults in case we do not provide a value for these.

MongoDB will find items quickly on fields that are indexed. If we end up searching something that is not indexed, MongoDB must search through the entire list of documents. Since we must be able to search quickly across different fields, we have to use indexes.

```javascript
//
internals.plugin.index({
  name: 1,
  description: 1,
  authors: 1,
  keywords: 1
});
```

Now for users, they should have a username, possibly a display name, an email address, create/update timestamps, and a list of likes. Since we're using MongoDB, data should be denormalized (meaning they should be grouped instead of split into separate tables). The plugin "Likes" makes sense to associate with Users exactly basically has a list of likes.

```
var internals = {};

internals.user = new Mongoose.Schema({
  'username': { type: String, required: false },
  'name': { type: String, required: false },
  'email': { type: String, required: false },
  'updated_at': { type: Date, default: Date.now },
  'created_at': { type: Date, default: Date.now },
  'likes': [internals.plugin]
});

var user = Mongoose.model('user', internals.user);
```

# SEARCHING PLUGINS

The most crucial part of the haki-plugins.com application is the ability for users to search for plugins. The visitor may want to search for a plugin by name if they know. They may only know what a plugin "needs" to do and search for a keyword or word that may be in the description. Finally, visitors that know who created the plugin, so they can search for all plugins made by that author.

The logic for accommodating this is a little complicated. It involves generating a MongoDB query that simultaneously the query across all of the relevant fields. In the example below, it is generating a MongoDB query matching our criteria and executing it.
