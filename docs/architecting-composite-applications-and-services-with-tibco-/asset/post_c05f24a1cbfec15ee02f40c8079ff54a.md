
are readily readable. Two common conventions that satisfy this criterion are

- Non-leading capitals: Each word in a field other than the first begins with a capital letter, such as `ClaimService` (for a type) or `claimService` (for an instance). The leading capital should be determined by whether the field references a type or an instance (see previous section).
- All letters are capitalized, and an underscore (_) or other separator is used between words, for example, `CLAIM_SERVICE`. This convention pretty much requires that an additional term be used to distinguish types from instances (see previous section).

One convention to be avoided is the use of all capitals with no special characters allowed (e.g., no underscores). Such a convention leads to names like CLAIMSERVICE, which is not only hard to read but also may lead to ambiguities.

## Best Practice: Plan for Multi-Word Fields

Adopt a convention for capitalizing names that ensures that the resulting multi-word names are readily readable.

## Use a Distinct WSDL Namespace URI for Each Interface

To avoid naming conflicts among the messages, ports, and operations of different interfaces, each interface should have its own namespace URI. Equally important, using distinct namespace URIs makes it possible to independently version the interfaces. This will facilitate the graceful evolution of interfaces in the environment.

## Best Practice: Use a Unique WSDL Namespace URI for Each Interface

Define each interface in a separate WSDL, and use a unique namespace URI for each WSDL.

## Incorporate Interface Major Version Numbers

In keeping with the versioning best practices outlined in Chapter 7, wherever the interface name is incorporated into certain naming structures, the interface's <major> version number should be appended to the interface name in those structures. This affects the following items:

- WSDL namespace URLs
- Schema namespace URLs when the schema is dedicated to a specific WSDL (see the section, “Schema Types Specific to an Interface and an Operation” later in this chapter)
- WSDL filenames (also include the interface's <minor> version number, as per versioning best practices)
- Schema filenames when the schema is dedicated to the specific WSDL (also include the interface's <minor> version number in the filename, as per versioning best practices)
- SOAP addresses (endpoints)
- SOAP action names

For simplicity, the version numbers are omitted from the examples in the following sections.

## Applying Naming Principles

## Idealized Name Structures

Given the structured name design principles laid out above, an idealized form of structure for naming service operations might have the following structure:

```
<functionalContext><abstractService><interfaceName>
<operationName>²
```

2. In a WSDL the scope of an operation name is the portType (WSDL 1.1) or interface (WSDL 2.0).

In practice, the enterpriseID is almost always defined using an Internet domain name. For example,

```
nouveau.com
```

Most often the enterprise ID occurs in the context of a URL or URI and has the form

```
http://nouveau.com
```

Many businesses have more than one line of business, with each line of business essentially operating as a separate company (particularly from an IT perspective). When this occurs, it is good practice to include the line of business as part of the <functionalContext>. This helps avoid name conflicts among similar functional areas (e.g., sales, human resources, finance) in the different lines of business of the same company. The result is

```
<functionalContext> ::= <enterpriseID><lineOfBusiness>
<functionalArea>
```

Consider Nouveau Health Care and the possibility that it might have two very different lines of business. One is an insurance provider, and the other is an online pharmacy. The idealized enterprise identifiers for Nouveau would then be

```
com.nouveau.insurance
com.nouveau.pharmacy
```

In transforming the idealized form into the form needed for a URL or URI, you have two choices, depending upon whether or not you want the line-of-business name to be part of the Internet domain name or the path. If you want it to be part of the Internet domain name, you end up with

```
http://insurance.nouveau.com
http://pharmacy.nouveau.com
```

If you want the line of business to be part of the path, you end up with

```
http://nouveau.com/insurance
http://nouveau.com/pharmacy
```

This, in practice, may not be an arbitrary choice: Making the line of business part of the Internet domain name allows distinct machines to be used as targets for the different lines of business; making the line of business part of the path forces a single machine to be used as the entry point for both lines of business. There may be organizational and management issues involved. These are discussed later in this chapter in the Complicating Realities section.

To deal with this type of situation, many enterprises employ network appliances that can make seamless conversions between these two formats. Although this adds flexibility, it requires network configuration—yet another administrative task.

## Best Practice: Global Uniqueness

Include an enterprise-specific qualifier to the functional context. If the enterprise has independent lines of business, include the line of business in the functional context as well.

## A Notational Convention for Internet Domain Names

This question of how much of the idealized name will become part of the Internet domain name occurs so often that we will adopt a convention for indicating the answer: The portion of the idealized structure that will become the Internet domain name will be outlined with a border. Using this convention, the example of the line-of-business name being part of the Internet domain name would be idealized as

```
<enterpriseID><lineOfBusiness><functionalArea>
```

The example of the line-of-business name being part of the path would be idealized as

```
<enterpriseID><lineOfBusiness><functionalArea>
```

## WSDL and XSD Namespace URIs

The idealized structure for a WSDL namespace URI has the form

```
<functionalContext><abstractService><abstractInterface>wsdl
<wsdlName>
```

Expanding the functional context, we have

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService>
<abstractInterface>wsdl<wsdlName>
```

It is common practice to make the actual name structure a URI. For the Payment Manager service’s Claim Payment interface WSDL and including the major version number in the name, this gives

```
http://insurance.nouveau.com/finance/paymentManager/
claimPayment/wsdl/claimPayment1
```

The idealized structure for a schema namespace URI has the form

```
<functionalContext><abstractService><abstractInterface>schema
<schemaName>
```

Expanding the functional context, we have

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService>
<abstractInterface>schema<schemaName>
```

It is common practice to make the actual name structure a URI. For the Claim Payment schema associated with the Claim Payment WSDL and including the schema major version number, this gives

```
http://insurance.nouveau.com/finance/paymentManager/
claimPayment/schema/claimPayment1
```

## Best Practice: WSDL and Schema Namespace URIs

Include the full functional context, abstract service name, abstract interface name, and WSDL or schema name in the WSDL and schema namespace URIs. Insert wsdl or schema prior to the WSDL or schema name to differentiate WSDL and schema namespaces.

## WSDL and XSD Filenames

It is a good practice to use the WSDL or schema namespace structure as the basis for defining the structure of the filename (i.e., the path to the file). The idea is to make the fully qualified filename a URL (or at least a URI). Making it a URL tells you where to locate the file. With this approach, the idealized structure for a filename is

```
<enterpriseID><lineOfBusiness><functionalArea><abstractService
<abstractInterface>wsdl<filename>
<enterpriseID><lineOfBusiness><functionalArea><abstractService
<abstractInterface>schema<filename>
```
