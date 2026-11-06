for the data type, one for the allocation scheme:

```
```
template <typename Data, typename Scheme>
class Storage ...
```
```

To use the class Storage we would then write, e.g.:

```
```
Storage<string, NewAlloc<string>> storage;
```
```

Using `Storage` this way is fairly complex and potentially error-prone, as it requires the user to specify the data type twice. Instead, the allocation scheme should be specified using a new type of template parameter, not requiring the user to specify the data type required by the allocation scheme. This new kind of template parameter (in addition to the well-known *template type parameter* and *template non-type parameter*) is called the *template template parameter*.

# ## 22.4.2 Policy classes - II: template template parameters

Template template parameters allow us to specify a *class template* as a template parameter. By specifying a class template, it is possible to add a certain kind of behavior (called a *policy*) to an existing class template.

To specify an allocation *policy*, rather than an allocation type for the class `Storage` we rephrase its class template header: definition starts as follows:

```
```
template <typename Data, template <typename> class Policy>
class Storage...
```
```

The second template parameter is new. It is a *template template parameter*. It has the following elements:

+   - The keyword `template`, starting the template template parameter;
+   - The keyword `template` is followed (between pointed brackets) by a list of template parameters that must be specified for the template template parameter. These parameters *may* be given names, but names are usually omitted as those names cannot be used in subsequent template definitions. On the other hand, providing formal names may help the reader of the template to understand the kind of templates that must be specified with the template template parameter.
+   - Template template parameters must match, in numbers and types (i.e., template type parameters, template non-type parameters, template template parameters) the template parameters that must be specified for the policy. This can be tricky, as some templates use default parameters that are hardly ever changed (like the allocation schemes for containers). Programmers may not immediately realize that these defaults exist and be confused when the compiler rejects such templates when trying to pass them as template template parameters for which these additional (default) parameters weren’t specified. However, the C++11 standard offers a solution for this problem in the form of *template aliases*, introduced in section **22.5**.
+   - Following the bracketed list the keyword `class` *must* be specified. In this case, `typename` can *not* be used.
+   - All parameters may be provided with default arguments. This is shown in the next example of a hypothetical class template:

```
```
    template <
        template <
            typename = std::string,
            int = 12,
```
```