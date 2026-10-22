access to JSON parsing libraries. Although this may theoretically be an issue, in practice it is less so.

At the time of this writing, JSON doesn't tend to be stored directly on disk.¹ at least not as often as XML is. Instead, JSON usage tends to be focused on transient usage, as in a response to a single request.

In fact, the typical use case for JSON is one where the same server provides both the client application (in the form of JavaScript) and the server implementation that responds to client requests. In such a setup, the ActiveRecord from_json and to_json are quite appropriate. Generally, such setups rely only on two of the HTTP methods: GET and POST.

# SOAP

Theoretically, SOAP is just XML with three element names standardized and with a uniform fault response defined. In practice, there is a large amount of supporting infrastructure available in Java and C# for consuming and producing SOAP, and this infrastructure tends to define the typical usage.

That machinery is optimized for statically typed languages and relies heavily on schemas. Requests and responses produced by this machinery tend to be more verbose and less human-readable than handcrafted XML.

Request and response sizes tend to be in a similar range as XML, though requests in SOAP (which tend to be POSTed as XML documents instead of using HTTP GET) may be a bit smaller. When used in an RPC style, parameters are matched by name.

Although best practice is to define one's schema prior to producing any code, in practice XML schema is too hard to produce correctly by other means, and schema generators that selectively expose internals from running code have proven to be too attractive; therefore, most SOAP-based web services are defined in this way. The client stub is then generated from this schema, which results in a fairly tightly coupled system. This may be suitable for controlled business intranets. On the Internet, not so much.

One area where SOAP shines is in certain areas of security, because a number of the best minds of the planet have worked out details for one-way messaging over alternate transports involving nonrepudiable signatures and federated identity. These extensions, however, are optional and are not available for every platform.

You can enable SOAP support in Rails via gem install actionwebservice. This support does not provide advanced functionality such as one-way messaging, alternate transports, nonrepudiable signatures, or federated identity.

1. CouchDB is a notable exception.