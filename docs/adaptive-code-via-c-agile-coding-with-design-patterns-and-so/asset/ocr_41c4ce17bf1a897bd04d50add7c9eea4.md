that the offending code will be fixed before shipping. This is why it is so important to unit test contracts. If a contract violation is not fixed before shipping and an end user is unfortunate enough to trigger an exception, it is most likely the best course of action to force the application to close. It is advisable to allow the application to fail because it is now in a potentially invalid state. For a web application, this will mean that the global error page is displayed. For a desktop application, the user can be shown a friendly message and be given a chance to report the problem. In any and all cases, a log should be made of the exception, with full stack trace and as much context as possible.

The next section covers the rest of the LSP’s rules—those that apply to covariance and contravariance.

# Covariance and contravariance

The remaining rules of the Liskov substitution principle all relate to covariance and contravariance. Generally, *variance* is a term applied to the expected behavior of subtypes in a class hierarchy containing complex types.

# Definitions

As previously demonstrated, it is important to cover the basics of this topic before diving in to the specifics of the LSP’s requirements for variance.

# Covariance

Figure 7-4 shows a very small class hierarchy of just two types: the generically named Supertype and Subtype, which are conveniently named after their respective roles in the inheritance structure. Supertype defines some fields and methods that are inherited by Subtype. Subtype enhances the Supertype by defining its own fields and methods.