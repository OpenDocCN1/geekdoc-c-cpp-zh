# Built-in handlers

# File

File handlers are used to generate static endpoints for serving up files. You are likely to use this with single files that don't fit in the directory handler explained shortly.

We are using the file handler to serve up the favicon, or the little specific icon that browsers use to associate a website.

We add the favicon to our lib/routes.js file as follows:

```
```javascript{
  method: 'GET',
  path: '/favicon.ico',
  handler: Controllers.Static.favicon
}
```
```

There are multiple ways of using the file handler, all of which involve modifying lib/controllers/handlers/static.js in our particular setup.

# STRING

This is how we're using the handler for hapi-plugins.com and is the most straight-forward approach.

```
```javascript{
exports.favicon = {
  file: dirname + '../../public/favicon.ico'
};
```
```

# CALLBACK

A callback takes the request object as an argument that returns the absolute or relative path.

```
```javascript{
exports.favicon = {
  file: function (request) {
    return dirname + '../../public/favicon.ico'
  }
};
```
```

# OBJECT

An object with several options.