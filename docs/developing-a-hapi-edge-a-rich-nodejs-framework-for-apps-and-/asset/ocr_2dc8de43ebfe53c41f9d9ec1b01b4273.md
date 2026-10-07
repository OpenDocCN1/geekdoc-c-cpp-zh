# CHAPTER 8: Models

```
internals.plugin.statics = function (queryString, sort-
String, callback) {
 var query = {};
 if (queryString && queryString.length > 0) {
 var pattern = new RegExp(queryString, 'ig');
  query = {
    '$or': [
      ('name': pattern),
      ('description': pattern),
      ('author': pattern),
      ('authors': {
        '$regex': pattern
      }},
      ('keywords': {
        '$regex': pattern
      })
    ]
  };
}
 var sortOrder = 1;
 var sortBy = sortString || 'name';
 if (sortBy[0] === '-') {
 sortOrder = -1;
 sortBy = sortBy.slice(1);
}
 var sort = {};
sort[sortBy] = sortOrder;
return this.find(query).sort(sort).exec(callback);
```

There is a lot going on in the search function above. The first function accepts two important arguments and a callback where the results will be sent.
The first is the query made by the user. We take the query and match it with all the relevant fields: name, descriptions, author, authors, and keywords.
The second argument determines sort order. When we grab results from the database, it has to know what to return (ascending or descending and by what field). We are using the convention of "-name" to mean descending by name and minus sign, "-", to mean ascending. If sortString is null, we default to name ascending.
We take these two arguments and execute a find query on the database.
Now, back in the controller, we define a search handler to use our new database search method. In this handler, we will also validate and sanitize the inputs to make sure no invalid or malicious inputs are entered.

```
module.exports.search = {
 validate: {
  query: {
```

104