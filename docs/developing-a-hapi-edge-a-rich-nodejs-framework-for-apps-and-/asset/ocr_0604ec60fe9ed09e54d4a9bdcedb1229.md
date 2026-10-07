# Schemas

# MongoDB::mongodb

Schemas are not really applicable when using the mongodb driver. For any applications that require some schema validation, please use Joi to provide some validation before inserting or ordering documents.

```
var Joi = require('joi');

var internals = {};

internals.plugin = Joi.object().keys({
  'name': Joi.string().required(),
  'description': Joi.string().optional(),
  'version': Joi.string().required(),
  'authors': Joi.array().optional(),
  'license': Joi.string().optional(),
  'repository': Joi.string(),
  'homepage': Joi.string(),
  'updatedAt': Joi.date(),
  'createdAt': Joi.date(),
  'keywords': Joi.array(),
  'dependencies': Joi.array(),
  'dependents': Joi.array(),
  'stats': Joi.object().keys({
    'releases': Joi.string(),
    'downloads': Joi.string(),
    'downloads_this_month': Joi.string(),
    'open_issues': Joi.string(),
    'pull_reqs': Joi.string()
  })
n});
```

// Use it later
var pluginToAdd = {name: 'hapi', ...};
Joi.validate(pluginToAdd, internals.plugin, function (err, value) {


```
if (err) {
  throw err; // invalid schema
}

var collection = mongodbClient.collection('plugin');
collection.insert(pluginToAdd, function (err, result) {
  if (err) {
```