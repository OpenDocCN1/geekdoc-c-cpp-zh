# 29 Using JSON

Using JSON has become over the past few years the preferred way of exchanging data between remote resources and JavaScript-based clients. The JSON format<sup>24</sup> is actually a subset of the literal notations allowed by standard JavaScript. JSON has a few limitations but certainly boasts two significant advantages over XML:

+   - It’s more lightweight (less verbose).
+   - It does not require any particular client-side technology—besides JavaScript itself—to be interpreted and processed.

Nowadays, most server-side technologies provide facilities to encode any eligible data structure into a JSON string and decode such strings when they come in. Depending on your technology of choice, you may need to install an extra library (easily found through Google), but rest assured you’re covered with Ruby, PHP, Python, Java, ColdFusion, and ASP.NET, to name but a few.

JSON lets you encode regular, integer-indexed arrays and associative arrays (aka hashes, dictionaries, or maps). In the latter case, keys can be anything (as long as they’re quoted), and values can be numbers, strings (barring some escaping), Booleans, **null**, or regular/associative arrays, nested to any depth you need. Decoding it is easy, but producing a JSON string requires some coding, so most JavaScript frameworks do that for you. More often than not, they also provide JSON-specific behavior for Ajax requests, as an extra convenience.

Note that JSON is supposed to be reasonably secure, which is why it doesn’t serialize functions. A valid JSON string always boils down to an inert object literal that, when run/interpreted, cannot do any harm by itself. However, if what you get is *not* a valid JSON string—and embeds a malicious function call—you’re at risk. This is why most JSON-parsing features offer an option to check/sanitize the string before running it.

This book’s code features an example page that fetches a JSON system info object through Ajax and populates a table row with it, using a couple neat tricks. You should check it out!

One of the main ways to use JSON these days is a small trick called JSON-P, which results in passing a JSON object to a callback function predefined in a script. You’ll learn more about that in the next task.

> 24. As defined on http://www.json.org/