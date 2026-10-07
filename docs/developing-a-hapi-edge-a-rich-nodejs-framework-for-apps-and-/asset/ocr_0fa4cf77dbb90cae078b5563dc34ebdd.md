made into this parameter. Our method in the server route is a POST and this JSON object gets translated to the payload object.

You can see that validation is done on the payload. The password passed in the payload is a string of at least eight characters and is a required field. In addition, we're telling hapi that the response is expected to be a JSON structure with a success value of either true or false.

You may be asking yourself, why is response not the validate section? The validate section is strictly for inputs. This may not be obvious when you use hapi with joy. Output (the response) validation can be extremely important if you rely on another API for your work. Output validation gives you confidence that you are getting the right things from it.

As you've seen in our code so far, we like to have everything broken up and are using the config quite extensively. Because the validation schema can get quite long long we often put the validation rules in the internals variable.

The internals variable is the place to put top-level variables in a file. This prevents pollution in that scope. This is especially useful in cases where we have to access the schema in multiple different places to handle the validation. The example below demonstrates this.

```
var internals = {
pluginSchema: Joi.object().keys({
});

// Get plugin data
exports.get = {
  description: 'get plugin data for a specific plugin id',
  response: {
    schema: internals.pluginSchema
  },
  handler: function (request, reply) {
    //
    ...
  }
};
```

# Validation for hapi-plugins.com

Let's take a look at the search function for hapi-plugins.com.

```
module.exports.search = {
validate: {
  query: {
    q: Joi.string(),
    sort: Joi.string().optional(),
  }
}
};
```