# Chapter 7 Representation and meaning

+   * XML HyperText Markup Language (X) – an XML formulation of HTML that allows inclusion of formatted text in XML documents, which can therefore be parsed by general-purpose XML libraries. Note that HTML5, supersedes HTML4, isn't valid XML, and is best treated as an output format, rather than being used to store data.

+   * Scalable Vector Graphics (SVG) – this XML schema allows inclusion of 2D vector graphics into documents.

Although getting started with XML is quite easy, becoming an expert, and understanding all the pros and cons to the different ways in which data can be represented in XML, takes some considerable time. There's a whirlwind tour of some its basic properties in Box 7:6; however, to become an XML master, you'll need a proper tutorial.

# RDF

Whereas JSON and XML represent data as a hierarchy or tree, the Resource Description Framework (RDF) takes a much more general approach, and considers data as an arbitrary graph describing the relationships between things. In both JSON and XML examples, properties such as 'type' or 'id' are implicitly associated with our particular become, however they are nested within the fragment of JSON or XML that describes it. In RDF, data structures are created by explicitly describing all relationships between the different components. While this can end being extremely verbose (and you'd certainly not want to try reading the most vital RDF files as a human), it means that RDF can be used to describe things that don't naturally follow hierarchical structures.

The fragment of RDF encodes our HBA_HUMAN example in a style known as 'Notation3':

```
@prefix p: <http://www.example.org/sequence_details#>
<http://www.example.org/sequence_HBA_HUMAN>
p:type "protein"
p:description "Hemoglobin subunit alpha GS=Human sapiens PE=1 HBA1 SV=2"
p:sequence "MVLSPADKTNIWKKAGVGAHAGEALEERMISFFFTKTYFPHDLHSQAGVKHKGGVALTAMNAVDHFDIMINALASDHLHKRVDVFNSHLLCTYTLAEHHAVPASL"
```

This example makes three independent statements about the sequence HBAMAN: first it has type 'protein'; second, it has a textual description; and third, it has a specific sequence. You can think of these as forming three 'subject-predicate-object' clauses. Any of them could be added, or additional ones would be valid. As the RDF is read by a program, the different statements are linked together to form a graph of properties and relationships. RDF graphs can be interrogated using the SPARQL query language (SPARQL, pronounced 'sparkle') Protocol and RDF Query Language. The syntax of SPARQL, and the kinds of query operation it provides, are relatively simple, as the language only has to embody the 'subject-predicate-object'; but the behaviour of a SPARQL query can be hard to predict, as the amount of work to answer a query depends on the topology and scale of the graph than on the structure of the query.