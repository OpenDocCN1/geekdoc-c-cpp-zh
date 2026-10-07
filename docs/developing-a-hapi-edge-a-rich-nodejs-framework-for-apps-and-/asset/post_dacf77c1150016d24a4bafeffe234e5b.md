
# Best practices

```javascript
var name = Xss(request.payload.name);
return reply(name);

}
);
```

```javascript
var Joi = require('joi');
var Xss = require('xss');

var config = {
  validate: {
    payload: {
      name: Joi.string().required().min(1),
      email: Joi.string().optional()
    }
  },
  handler: function (request, reply) {
    var output = {};
    output.name = Xss(request.payload.name);
    output.email = '';
    if (request.payload.email) {
      output.email = Xss(request.payload.email);
    }
    return reply(output);
  }
};
```

Recall from Chapter 5 that joi can validate our inputs and output. As you can see in the above example, combining joi with xss, we can make our inputs secure to prevent against these types of attacks.

# CSRF

Cross-site request forgery (CSRF "see surf") is another vulnerability where an attacker is able to insert a script or link (using XSS) that causes the victim's browser to submit a form on a distinctly different but familiar website such as their bank website. The victim has expired cookies to trust bank website, the form may be accepted as if the victim intended it.

# SOLUTION

The bank website should generate a custom identifier on form load that is required in order to submit the form. Any blindly submitted form payloads will be rejected without this key. The victim would have to visit the form, fill out the elements, then submit in order to perform the attacker's desired effect.

# CHAPTER 12: Security

Use hapi's crumb module.

```javascript
// Server
var crumbOptions = {
  restful: false, // false enables payload level validation
  // crumb, true uses X-CSRF-Token header
  addToViewContext: true, // automatically add to view context
  isSecure: false // required if HTTPS is not used
};
server.register({ register: require('crumb'), options: crumbOptions }, function (err) {
  if (err) {
    return err;
  }
});

// View
<form action="submit" method="POST">
  <input name="crumb" type="hidden" value="{{crumb}}"/>
  <!-- -->
</form>
```

```javascript
// /submit Handler
handler: function (request, reply) {

  return reply('ok'); // Do not have to do anything different
}
```

# SSL

Many websites today run on bare HTTP instead of the more secure HTTPS. This performs all of the data transfer between browser to server in plain text on the network. Due to the ways networks work, anyone on same network can view all of the data transfer traffic and see passwords, URLs, messages, and more.

One of the easiest ways to add more security to a website is to force users to use SSL/HTTPS. This requires buying and installing certificates, but it will encrypt all of the traffic between browsers and servers.

There are many ways to configure SSL for a Node.js web server. The most common way is to use a reverse proxy like Apache or nginx/stunnel to handle the SSL certificates, terminate the encryption, and then forward the traffic to your Node.js service over unencrypted HTTP. This requires no change to a working hapi application. For information on how to nginx ssl termination, see DigitalOcean: How To Set Up Nginx Load Balancing with SSL Termination.

Alternatively, Node.js can terminate the encryption by processing the certificates, but this can be time consuming and increases load on application machines. For information on how to use ssl termination, see the API docs server.connection.tls option. Below is a basic example of enabling SSL termination in hapi:

```javascript
var fs = require('fs');
var options = {
  port: 443,
  key: fs.readFileSync(keyPath, 'utf8'),
  cert: fs.readFileSync(certPath, 'utf8')
}
server.connection(options);
```

# Header stripping

There are may vulnerabilities that can be fixed by either setting or removing an HTTP header. Before breaking down the vulnerabilities, it is a generic way to globally set or remove headers:

```javascript
server.ext('onPreResponse', function (request, reply) {
  if (!request.response.isBoom) {
    request.response.output.headers.ToAdd = 'someValue';
    delete request.response.output.headers.toRemove;
  }
  return reply();
});
```

Alternatively, this can be done within a single handler to apply just a single route:

```javascript
handler: function (request, reply) {
  return reply(output)
    .header('Content-Type', 'application/json')
    .header('X-Frame', 'DENY')
}
```

# CHAPTER 12: Security

# CLICKJACKING

Clickjacking occurs when your web page is inserted into an HTML iframe where users' clicks can be hijacked. If a user clicks on your home button, an attacker could hijack the click and redirect the user to a malicious webpage.

Solution

Setting the X-Frame header to 'DENY' will prevent browsers from allowing your web-pages from being put inside of a frame or iframe (<iframe>).

# X-POWERED-BY

Most web server frameworks, by default, announce in the HTTP header "X-Powered-By" what framework and version was used to generate the page.

By default, hapi does not do this.

SOLUTION

# X-Frame-Options

Modern browsers support a header called X-Frame-Options to prevent your site from being rendered in an <frame>, <iframe>, <object>, or <embed>. This is the primary defense against clickjacking.

Solution

Setting the X-Frame-Options header to 'DENY' will prevent browsers from allowing your web-pages from being put inside of a frame or iframe (<iframe>). Setting it to 'SAMEORIGIN' allows the page to be framed only by pages on the same origin.

# Content-Security-Policy

Content Security Policy (CSP) is a security layer that helps to detect and mitigate certain types of attacks, including cross-site scripting (XSS) and data injection attacks. It allows site operators to declare which dynamic resources (scripts, styles, images) are allowed to load on their page.

You can define a CSP by setting the Content-Security-Policy header. For example, a policy that only allows scripts from your own domain would be:

```javascript
reply.response().header('Content-Security-Policy', "script-src 'self'");
```

# SOLUTION

A robust CSP might include:

- default-src 'self'; (Restricts all resources to the same origin)
- script-src 'self' https://trusted.com; (Allows scripts from the same origin and a trusted domain)
- style-src 'self' 'unsafe-inline'; (Allows styles from the same origin and inline styles)
- img-src 'self' data:; (Allows images from the same origin and data URIs)

# Strict-Transport-Security

The Strict-Transport-Security (HSTS) header tells the browser that the site should only be accessed using HTTPS. This prevents protocol stripping attacks.

SOLUTION

```javascript
reply.response().header('Strict-Transport-Security', 'max-age=31536000; includeSubDomains');
```
