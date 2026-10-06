# Using the Regular-Expression Type Provider

As you know, the type provider is used to generate a new type with class members, such as methods and properties. HelloWorldTypeProvider generates class members from a predefined data schema. The predefined data schema in this case requires five methods and five properties. As software developers, we always look for something that can be created programmatically. Is there any way to create the class members from some variable passed in by a user? The answer is “Yes.” The regularexpression type provider dynamically generates class members based on a regular-expression parameter passed in a user, as shown in Listing 5-8.

+   LISTING 5-8 Invoking a regular-expression type provider

```
type T = Samples.ShareInfo.PTest.RegularExpressionTypeProvider<
"^(?<AreaCode>\d{3})-(?<PhoneNumber>\d{3})-\d{4})$$"
let reg = T()
let result = T.IsMatch("425-555-2345")
let r = reg.Match("425-555-2345").AreaCode.Value
```

The first line in the listing shows how the type provider shows the parameters between < and >. This is the most common way for a type provider to get parameters. The third line a static method, but this is not a problem because ProvidedMethod can be IsStaticMethod = true. last line is the most interesting part. The Match function returns a variable that has an AreaCode property. The AreaCode property does not look like any generic .NET property. It is a generated property from the regular-expression group AreaCode. From the preceding analysis, something is needed to take and interpret the regular-expression pattern string and the type provider needs at least two. One is the type-provider, and the other is a type with an AreaCode property.

First need to get the regular-expression pattern string. To parameterize the type provider, you pass a list of ProvidedStaticParameters containing the name and type of each parameter to the DefineStaticParameter method along with an instantiation callback, as shown in Listing 5-9. At runtime, the user supplies for each static parameter will be passed into the second argument of the callback function in the same order they were defined.

+   LISTING 5-9 Getting the type-provider static parameter

```
let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]

doo newT.DefineStaticParameters(
parameters=staticParams,
instantiationFunction=(fun typeName parameterValues ->
...
))
```