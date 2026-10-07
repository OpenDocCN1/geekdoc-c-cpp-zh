```
auth: 'YourCookieAuth'
));
server.route({
  method: 'GET',
  path: '/login',
  handler: login,
  config: {
    auth: 'YourThirdPartyAuth'
  }
});
server.route({
  method: 'GET',
  path: '/logout',
  handler: logout,
  config: {
    auth: 'YourCookieAuth'
  }
});
server.start(function () {
  console.log('Started...');
});
```

You can see here that logout and private routes are protected by cookies still. We have a public handler for /public resources, which may be a generic login page like we had in our cookie example. Finally, we have a login page, which goes to the third party authentication site (github) to get a token. Bell does this magic for you and once you have that, the cookie will be generated. You will not need to login again until your session expires. More details on the specifics of the providers bell supports to bell.

# Summary

In this chapter we explored some basic options that are available for authentication with hapi. The basic authentication strategy can be useful for applications that are protected by a firewall and are internally facing.
The cookie authentication strategy is likely more useful, especially for building sites that require a session. Combining the cookie authentication strategy with bell gives you a very robust authentication solution. One of the nice things about hapi is that it supports a mix of any of these and other authentication strategies to fit the needs of the application you are building. Whatever the choice is, rest assured that the creators of hapi and the community at large have tested and support many varying of authentication strategies.