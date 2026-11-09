The DoS service is very new, and it's likely to evolve rapidly. In the current release of App Engine, you configure the DoS service by putting a file into your application configuration, which specifies the contents of the blacklist. In a Python application, you create a file named dos.yaml containing a list of blacklist entries. The entries are, unfortunately, currently completely unreadable. They're based on a standard routing notation for the IP called CIDR (classless inter-domain routing). You'll need to look up CIDR notation to be able to write it. For example, to say “all addresses starting with 192.168.0.” you'd write “192.168.0.1/24”.

So, for example, in Python, if you were under a DoS attack coming from the IP network block containing 192.168.72.12, you'd put the following into dos.yaml:

```
```
blacklist:
- subnet: 192.168.72.12/22
```
```

As I said, the DoS protection service is a new addition to App Engine, so it's likely to have evolved by the time you read this. But the basic concept will be the same: you define who needs to be blocked and put that into a file in your application configuration. For the details, you'll definitely want to look in the up-to-date documentation on the App Engine website.

Now you know what you're up against. In this section, we've looked at the threats that you need to consider—the ways that malicious people on the net can attack your service and how you can protect yourself against them.

In this chapter, we've taken a very shallow look a security. Security is an important, complicated concern that cuts across all of the other aspects of building a web service. As we've seen, conceptually building a secure application or service isn't difficult, but practically it's close to impossible.

The starting point of any security system is the security policy—the rules that describe the objects manipulated by your application/service and who is allowed to access and/or manipulate each object. We've seen an example of a security policy for our chat application, defined in terms of chat rooms and users. Care in designing this policy is critical; we saw an example of providing a view that wasn't covered by policy can completely negate the policy.

Once you have a security policy designed, you need to implement it. It's critical to do this carefully. You need to consider every aspect of