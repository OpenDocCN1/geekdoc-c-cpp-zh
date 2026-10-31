
## Name Structures Define Search Strategies

In SOA, the structure of a name not only identifies the item being named, but often indicates how to find the item. When people are looking for an artifact, they often begin with only a vague notion of what they are looking for. While indexes and keyword associations can be of use, the structure of the name implicitly defines a search strategy for locating items. Consider, for example, the Nouveau Health Care Payment Manager’s Claim Payment Interface. Its WSDL might have the URL

```
http://insurance.nouveau.com/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl
```

This name not only uniquely identifies the WSDL file, it tells us where to find it: Go to the machine designated by insurance.nouveau.com (at the default port 80), look in the finance/paymentManager/claimPayment/wsdl directory, and obtain the file claimPayment.wsdl.

## Name Structures Define Routing Strategies

Although it is not formally a part of the web services paradigm, ports (endpoints) often make use of names in directing service requests to the actual service provider. The component (and often the machine) that accepts service requests is often different than the component actually servicing those requests. Appropriate naming can aid the receiving component in routing requests to the provider.

For example, the port (endpoint) address (the address to which service requests are directed) is designated by a URI, which is a form of name. Consider the address of the claim payment interface for Nouveau Health Care, given as

```
https://insurance.nouveau.com:443/finance/paymentManager/claimPayment
```

Also consider the address of the claim submission interface, given as

```
https://insurance.nouveau.com:443/claims/claimRouter/claimSubmission
```

The actual component to which both kinds of requests are directed is designated by the first part of the address URI, namely the domain name and port (not to be confused with the WSDL concept of port):

```
https://insurance.nouveau.com:443
```

This indicates that requests are received on port 443 of the machine designated by insurance.nouveau.com. From there, if the requests are to be serviced by another component, they must be routed to the actual service provider. The presence of the URI path structure in the address below the Internet domain name and port number makes it possible to route requests arriving at port 443 based on this path. Alternately, this information can be ignored and all requests can be routed to a common destination that provides support for all web services sharing the domain name and port.

In contrast, both addresses could have been given as

```
https://insurance.nouveau.com:443
```

In this case, since the path is absent, there is no information that can be used to route requests.

Using the structure of the address is, of course, not the only way to route. Other information such as the soapAction, the structure of the WSDL namespace URI, and the port/operation naming structure underneath it can also be used for routing. Regardless of which names are being used, the structure of these names and the consistency with which that structure is used can greatly simplify the routing of service requests.

## What Needs a Name?

In an SOA environment there are many things that require names. These include

- WSDL-related names:
    - The WSDL itself (the name attribute in the top-level `<definitions>` tag).
    - The WSDL filename.
    - The targetNamespace defined by the WSDL (also in the top-level `<definitions>` tag). This name is a URI, and is the logical prefix for the name of each entity defined in the WSDL.
    - The entities defined by the WSDL: services, port types (interface), operations, messages, bindings, and ports (endpoints).
    - The soapAction.
    - The schemaLocation of each imported XSD file.
    - The address of each service port (endpoint).
- Schema-related names:
    - The XSD filename (if the schema is not embedded in a WSDL).
    - The targetNamespace defined by the schema (either embedded in the WSDL or a stand-alone XSD). This name is a URI and is the logical prefix for the name of each entity defined in the schema.
    - The entities defined by the schema: types, elements, and attributes.
    - The schemaLocation of each imported XSD file.
- JMS-related names:
    - Static destination (topic or queue) names
    - EMS server names
- SCA-related names:
    - Composite names
    - Component type names
    - Service names

Some of these items are actual artifacts, such as files. Others are simply logical names for definitions (port types, messages, elements, etc.) or groups of definitions (namespace URIs). All of them will have to be dealt with by the producers and consumers of services. These names, and the standards for defining them, are the focus of this chapter.

## Structured Name Design Principles

### Use a General-to-Specific Structure

Structured names (think www.nouveau.com) are trees. The root of the tree represents the entire tree. Each node below represents a subtree rooted at that node. The root of the Internet (the parent of com) is not explicitly named, but the next tier down in the Internet naming system (referred to as top-level domains) consists of nodes such as .com, .net, .org, and .edu. Within each of those domains there are subdomains whose names are meaningful only in the context of the parent domain. Thus for uniqueness you refer to nouveau.com rather than just nouveau (which has different meanings in .com, .net, .org, etc.).

Because of the inherent tree structure, it is important that the logic of the structure you define be organized around a true hierarchy. The outline of such a hierarchy for services derives from the description of a service presented in the concepts discussion earlier. From the abstract concept discussion we have

```
<functionalContext><abstractService><abstractInterface>
```

This is a general-to-specific structure. A functional context may contain more than one service, and each service can contain more than one interface. Conversely, services are specific to a particular functional context, and each interface is specific to a particular service.

Ideally, the actual hierarchy is represented by a uniform sequence of fields in a left-to-right, most-general-to-most-specific fashion. This is the pattern you see in the naming of Java classes:

```
com.nouveau.insurance.finance.paymentManager.claimPayment.payClaim
```

Here com.nouveau.insurance.finance represents the functional context. The abstract service is represented by paymentManager. The abstract interface is represented by claimPayment.payClaim, the interface and operation used for paying a claim. Note that there is hierarchical structure both within the functional context and within the interface.

Unfortunately, many names in the SOA world are required to be URIs or URLs. These include namespace names and WSDL/SOAP address and soapAction fields. The structuring scheme for URIs does not strictly adhere to a uniform principle. Each URI or URL actually contains two name hierarchies, each with different construction rules. Consider the earlier example:

```
http://insurance.nouveau.com/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl
```

There are three parts to this string involving two different name structures:

1. `http://`, the first part, represents a protocol to be used to access the artifact. From a name structure perspective, we can ignore this.
2. `insurance.nouveau.com`, the second part, is an Internet domain name that designates a machine on the Internet. In the Internet domain name, hierarchy is read right to left.
3. `/finance/paymentManager/claimPayment/wsdl/claimPayment.wsdl`, the third part, is called the path. It represents a name hierarchy local to the machine designated by the Internet domain name. The path name hierarchy is read left to right.

What makes the use of two different name hierarchies and their differences in right-to-left and left-to-right reading unambiguous is the use of two different field separators. The Internet domain namespace fields are separated by a period (.), while the local namespace fields are separated by a forward slash (/). The occurrence of the first slash to the right of the Internet domain name is the clue that you have switched naming hierarchies.

If you wanted to make this namespace uniform, reading entirely left to right, you would have to switch the order of the Internet namespace elements:

```
com.nouveau.insurance.finance.paymentManager.claimPayment.wsdl.claimPayment.wsdl
```

This is, of course, the kind of structure used for naming Java classes.

### Best Practice: General-to-Specific Structure

When the structure of names is not already constrained, establish a uniform left-to-right, general-to-specific hierarchical structure for names following the pattern

```
<functionalContext><abstractService><abstractInterface>
```

When the structure of names is partially constrained (e.g., URLs and URIs), apply this principle to the lower-level structure of the names (i.e., the path in the URL or URI).

### Employ Hierarchical Naming Authorities

Names, to be useful, must be unique. Uniqueness requires that some authority keep track of which names have been assigned so that newly issued names can be assured to be different. Unfortunately, having a single authority to keep track of all names is impractical, particularly for names with global scope.

The systems that have evolved (in numerous places) to address this issue involve the use of hierarchical authorities. This strategy involves two elements. The first is a standardized syntactic structure for defining names as sequences of fields. The Internet domain name structure (e.g., insurance.nouveau.com) is one example.
