§23.3 Type Checking: The basic rules of type equivalence and type checking as they apply to templates.
§23.4 Class Template Members: How members of a class template are defined and used.
§23.5 Function Templates: How to define and use function templates. How overloading is resolved for function templates and ordinary functions.
§23.6 Template Aliases: Template aliases provide a powerful mechanism for hiding implementation details and cleaning up the notation used for templates.
§23.7 Source Code Organization: How to organize templates into source files. Chapter 24, Generic Programming, presents the basic technique of generic programming, and the fundamental idea of concepts (requirements on template arguments) is explored:
§24.2 Algorithms and Lifting: An example of the basic technique for developing a generic algorithm from concrete examples.
§24.3 Concepts: Introduces and discusses the fundamental notion of a concept, that is, a set of requirements that a template can impose on its template arguments.
§24.4 Making Concepts Concrete: Presents techniques for using concepts expressed as compile-time predicates.
Chapter 25, Specialization, discusses template argument passing and the notion of specialization:
§25.2 Template Parameters and Arguments: What can be a template argument: types, values, and templates. How to specify and use default template arguments.
§25.3 Specialization: Special versions, called specializations, of a template for a specific set of template arguments can be generated from the templates by the compiler or be provided by the programmer.
Section 23.1
Chapter 26, (instances) and name binding:
§26.2 Template Instantiation : The rules for when and how a compiler generates specializations from a template definition and how to specify them manually.
§26.3 Name Binding: The rules for determining to which entity a name used in a template definition refers.
Chapter 27, Templates and Hierarchies, discusses the relation between the generic programming techniques supported by templates and the object-oriented techniques supported by class hierarchies. The emphasis is on how to use them in combination:
§27.2 Parameterization and Hierarchy: Templates and class hierarchies are two ways of representing sets of related abstractions. How do we choose between them?
§27.3 Hierarchies of Class Templates: Why it is usually a bad idea simply to add template parameters to an existing class hierarchy?
§27.4 Template Parameters as Base Classes: Presents techniques for composing interfaces and data structures for type safety and performance.
Chapter 28, Metaprogramming, concentrates on the use of templates as a means of generating functions and classes:
§28.2 Type Functions: Functions that take types as arguments or return types as results.
§28.3 Compile-time Control Structures: How to express selection and recursion for type functions, and some rules of thumb for their use.
§28.4 Conditional Definition: enable_if: How to conditionally define functions and overload templates using (almost) arbitrary predicates.