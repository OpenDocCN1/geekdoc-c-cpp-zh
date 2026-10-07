
## CHAPTER 8: Models

```javascript
'last-day': function (_module) { return '/downloads/range/last-day/' + _module },
'last-week': function (_module) { return '/downloads/range/last-week/' + _module },
'last-month': function (_module) { return '/downloads/range/last-month/' + _module },
'last-year': function (_module) {
    var today = new Date();
    var from = [today.getFullYear() - 1, today.getMonth() + 1, today.getDate()].join(':');
    var to = [today.getFullYear(), today.getMonth() + 1, today.getDate()].join(':');
    var dateRange = [from, to].join(':');
    return '/downloads/range/' + dateRange + "/" + _module;
};
```

```javascript
internals.NpmDownloads = function (options) {
    this.options = Hoek.applyToDefaults(internals._defaults, options || []);
    return this;
}

internals.NpmDownloads.prototype.getDownloadsBy = function () {};
internals.NpmDownloads.prototype.lastDay = function () {};
internals.NpmDownloads.prototype.lastWeek = function () {};
internals.NpmDownloads.prototype.lastMonth = function () {};
internals.NpmDownloads.prototype.lastYear = function () {};
```

module.exports = internals.NpmDownloads;

Next, we will out a function for calling the downloads request. Unlike the previous function, this returns a function that we use to generate the other requests. The other functions basically become wrappers for getDownloadsBy.

```javascript
// /
internals.NpmDownloads.prototype.getDownloadsBy = function (_type, range) {
    var self = this;
    return function (moduleName, callback) {
        var method = "GET";
        var uri = self.options.host + self.options.uris[range](moduleName);
```

```javascript
var options = {
  redirects: 3,
  timeout: 30000,
  rejectUnauthorized: true
};
```

```javascript
var processResponse = function (err, body) {
  // Leave room in case response modification required
  return callback(err, body);
}
```

```javascript
var readResponse = function (err, res) {
  if (err) {
    return callback(err);
  }
  Wreck.read(res, json:true, processResponse);
};
```

```javascript
var req = Wreck.request(method, uri, options, readResponse);
// ...
```

Finally, we factor in getDownloadsBy for the remaining API methods by configuring only the differences between functions:

```javascript
// ...
internals.NpmDownloads.prototype.lastDay = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-day')(moduleName, callback);
};
```

```javascript
internals.NpmDownloads.prototype.lastWeek = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-week')(moduleName, callback);
};
```

```javascript
internals.NpmDownloads.prototype.lastMonth = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-month')(moduleName, callback);
};
```

```javascript
internals.NpmDownloads.prototype.lastYear = function (moduleName, callback) {
  return this.getDownloadsBy('point', 'last-year')(moduleName, callback);
} //
```

## PLUGINS Model: ACTUAL USAGE

Back in the handler, we want to combine the results between the NPM Package search results with an array of packages. Then, to ensure the list is unique by name. Then, for each unique module, we need to grab the full module data. Finally, we want to list this and add/update to the database.

To ensure uniqueness, we use a library called lodash the uniq function. We pass a list of just modules and it will strip out duplicates. But then, to start, we need to pull a list of here models.

```javascript
Async.parallel({
  shortlist: function (cb) { return NPMPackages.getShortList(cb); },
  hapiKeyword: function (cb) { return NPMPackages.getByByword('hapi', cb); },
  hapiKeyword: function (cb) { return NPMPackages.getKeyord('hapi', cb); },
  hapidotsjsKeyword: function (cb) { return NPMPackages.getByKeyword('hapi.js', cb); },
}, function (err, results) {
//..
```

As we have seen before, we are using the Async pattern to request four API calls at the same time and combine the results. This is important since we need the data from all four sources to identify which plugins are happy.

```javascript
var hapiKeyword = results.hapiKeyword.rows.map(function (module) {
  return module.key[1];
});
```

```javascript
var hapidjsKeyword = results.hapijsKeyword.rows.map(function (module) {
  return module.key[1];
});
```

```javascript
var hapidotjsKeyword = results.hapidotjsKeyword.rows.map(function (module) {
  return module.key[1];
});
```
