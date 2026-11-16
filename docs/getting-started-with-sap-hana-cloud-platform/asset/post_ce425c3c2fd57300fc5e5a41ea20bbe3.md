
straightforward to configure, right? However, if we go that way, then every individual user would have to grant access to the extension application. This is clearly not what we want in an enterprise environment.

## What Is SAP HCP Identity Propagation and How Does It Work?

As you learned in Chapter 8, Section 8.5, it’s fairly easy to configure SSO between an SAP HCP application and another system by using a common identity provider system. Whenever you request any of those systems for the first time, you’ll be presented with a login screen. After successful login, you’ll be redirected back to the original solution, supplying a signed SAML assertion confirming the successful login. Based on that, a subsequent web session is established.

The OAuth 2.0 SAML bearer assertion flow defines the process to use a SAML assertion to request an OAuth access token for a certain user, which is used to authenticate the user and perform OData API queries. All of that implementation is encapsulated in the SAP HCP Connectivity Service, making the whole process transparent for extension application developers.

From a development perspective, the code looks relatively simple:

```
Context ctx = new InitialContext();
HttpDestination destination =
(HttpDestination) ctx.lookup("java:comp/env/sap_hcmcloud_core_odata");
HttpClient client = destination.createHttpClient().execute(..)
```

As a result, the query will always execute on behalf of the currently logged in user without any need for the application to handle it.

## 11.3 Integration Points for Extending SAP Cloud Solutions

As Figure 11.4 and Figure 11.5 outline, a number of native artifacts are delivered with the extension application in order to find their way into the corresponding extended SAP Cloud solution during installation. Different SAP Cloud solutions currently allow integration of a different subset of the more generic list ahead. This section aims to provide an overview of what’s possible today without getting into particular details. By no means does the list pretend to be complete, but it should give you a general perspective on how serious SAP is about extensibility and making sure that corporate IT teams can be as productive with SAP Cloud solutions as they have been for the last 40-plus years with on-premise solutions. SAP will keep expanding the list as new SAP Cloud solutions integrate with SAP HCP.

As a general rule, SAP HCP is already able to import most of those artifacts into the solutions for which tighter integration is already in place. Enabling full coverage for all SAP Cloud solutions is planned with upcoming releases and is subject to integration API availability.

### 11.3.1 Custom Business Objects and Views

Most of the SAP Cloud solutions allow developers and administrators to create a limited number of custom business object definitions, which each solution handles differently. Some allow defining formatters or validators for the different fields, and others allow you to put in some metadata description outlining how the object will be visualized and to which screen it’ll be attached. With some of the solutions, it’s possible to define a simple workflow describing how that custom object is filled with data and what steps the data goes through. What is common among all solutions is that those objects are stored in the SAP Cloud solution database and become part of the solution’s object model.

The following are a few examples:

- In SuccessFactors, custom objects are managed by the Metadata Framework (MDF) as part of the solution object model. This is a key design principle from the first day MDF was introduced.
- In Ariba, it’s possible to create Ariba Query Language (AQL) views over the data stored in the solution. This feature is not exposed to customers yet.
- In all SAP Business ByDesign-based solutions, you can use the SAP Cloud Application Studio SDK and create new custom entities via business object definition language (BODL).
- In SAP Jam, you can register custom business objects in the form of external OData endpoints that are subsequently introspected for the list of available fields.

You typically have the flexibility to define the cardinality of how instances of the custom object relate to other entities in the solution object model. Custom object instances typically get exposed automatically for read and write via REST/OData API, unless explicitly specified otherwise.

### 11.3.2 Workflows

Every SAP Cloud solution has the internal notion of workflows (one or more), implementing a large variety of industry best practices. At the same time, almost none offer a programmatic way to interact with these workflows; beyond triggering a new cycle. However, there are some exceptions to the rule:

- SuccessFactors offers the ability to define MDF object workflows, defining how object data is to be filled. What's coming in late 2015 is programmatic access to the solution workflow engine, allowing developers to interact with the already defined standard workflows.
- For SuccessFactors performance management, it's already possible to shift a performance form to the next step via an API.
- SAP Business ByDesign-based solutions allow for defining new workflows and triggering existing ones. No modification of the existing predelivered workflow steps in the system is allowed.

### 11.3.3 Roles and Permissions

Many of the SAP Cloud solutions allow for the creation of custom security roles, and practically all allow administrators to manage the role assignments in groups via administration tools. Most of the solutions offer field-level security with fine-grained operations control (create/read/update/delete). What SAP HCP provides in that space for extension accounts is to enable transparent role assignment propagation to SAP HCP applications from the extended SAP Cloud solution. This allows administrators to keep on working in the original SAP Cloud solution, managing extension application role assignments from there the same way they do for standard product entities. SAP HCP already provides transparent role and permission checks for Java applications when extending SuccessFactors. The same level of integration is in the works for the other SAP Cloud solutions.

### 11.3.4 API Clients

In order to communicate with SAP Cloud solutions, SAP HCP needs registered API endpoints/client keys. The majority of SAP Cloud solutions support OAuth, some even with OAuth 2.0 SAML bearer assertions. This approach eliminates the need to hardcode service users and use static passwords. It provides flexibility to manage fine-grained access by controlling the issued OAuth access tokens. With identity propagation, SAP HCP is able to transparently call underlying SAP Cloud solution APIs on behalf of the logged in user, providing an end-to-end integrated experience for developers and end users.

In addition to pure data-access APIs, some SAP Cloud solutions also expose theming APIs, allowing you to generate consistent extension application UIs in line with the configured customer corporate branding in the extended SAP solution.

Last but not least, some of the SAP Cloud solutions provide a way for extension applications to register on their event bus and listen for events. This eliminates the need to have heavyweight, constant polling for updates, something that was generating needless load for the last few years.

### 11.3.5 Rules

Many SAP cloud solutions allow for configuring business logic when filling the fields of custom business object instances. Similarly, SAP Business ByDesign based solutions allow for defining field constraints and dependencies. SAP HCP naturally offers packaging and import of such rules for the solutions for which this is supported.

Using SAP Cloud Application Studio, developers are able to define association validation rules both during the creation and saving of data.

### 11.3.6 Configurable UIs

SuccessFactors in particular offers developers and administrators the ability to define configurable UIs so that you can specify which pages the object will be rendered in and in what form.

Another example is SAP Jam, which offers the possibility to provide a manifest that specifies how the different entities in an external OData business object are to be rendered.

### 11.3.7 Custom Code

Practically the only SAP Cloud business solution that allows full-featured custom code execution on the application stack is SAP Business ByDesign. Development is done using SAP Cloud Application Studio in an SAP-specific scripting language, allowing you to implement custom add-ons.
