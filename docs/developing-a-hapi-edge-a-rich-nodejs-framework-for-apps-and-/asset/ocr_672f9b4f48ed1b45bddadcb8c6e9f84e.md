# The request

If we log the output with console.log(request.query) then the result we'll
 printed to the console would show as:

```
{ hello: 'hi' }
```

It's worth noting that sometimes the value can be an array.hapi handles multiple query
keys automatically for you, you do have to be aware that the result can be a different
type than expected.
If the URL looks like the following:

```
http://localhost:8080/plugins/blipp?hello=hi&hello=hey
```

We now see the value as an array:

```
{ hello: ['hi', 'hey'] }
```

# payload

request.payload contains information that has been transmitted as part of the request
that's not suitable as a query. This may be a file, or a blob of JSON or XML. While it's cer-
tain possible to send payload for all of the request methods (GET, POST, DELETE, PUT,
PATCH, etc), it's typically used for GET. If you do end up seeing payload for GET,
y should probably rethink your design.
Let's start with a simple example for a handler where we'd utilize the POST method
of creating a new user.

```
handler: function (request, reply) {
  console.log(name is: ' + request.payload.name);
  console.log(email is: ' + request.payload.email);
  return reply('success');
}
```

If you recall when we talked about params earlier and the GET method, we wanted to
contrast this with payload. For the handler, we setup a route as below.

```
server.route({
  method: 'POST',
  path: '/user',
  config: {
    handler: handler
  }
});
```