```
exports.favicon = {
  file: {
    // a path string or function as described above
    path: __dirname + '/../../public/favicon.ico',
    filename: '??',
    mode: false,
    lookupCompressed: false
  }
};
```

Our path indicates where to find the file to serve up. This can also be set to the callback function as discussed above.

The filename is an optional filename to specify if spending a "Content-Disposition" header. This defaults to the basename of the path.

Mode specifies whether or not the "Content-Disposition" will be included. By default this is set to false, which means it's not included.

lookupCompressed, if true, looks for the same filename with the '.gz' suffix for a precompressed version of the file to serve if the request supports content encoding. It defaults to false.

# DIRECTORY

A more likely use-case than the file handler is the directory to serve up multiple files. It is common in order to serve files as images, CSS or JavaScript files used for the front-end.

Similar to our file handler, the route is set up in lib/routes.js and in this case, we're doing images and CSS as follows:

```
{ method: 'GET', path: '/css/{path}', handler: Controllers.Static.css },
{ method: 'GET', path: '/img/{path}', handler: Controllers.Static.img },
{ method: 'GET', path: '/js/{path}', handler: Controllers.Static.js },
// ...
```

The handler is defined in a way that's so similar that we're only going to look at the first one as an example:

```
exports.css = {
  directory: {
    path: __dirname + '/../../public/css',
    index: false
  }
};
```