You've seen how to create these global types at various points in previous chapters, so this section will focus on the additional options that can be maintained for these global types centrally and can then be inherited into programs automatically.

# ### 10.3.1 Data Elements

A *data element* describes an elementary data type or a reference data type. It allows you to maintain both technical and semantic attributes. *Semantic attributes* are significant for screen fields that refer to this data element. For example, the screen field can automatically import input help ([F4] help) or field help ([F1] help) from a data element. For ABAP data objects that refer to the data element, the semantic attributes hold no significance.

For an elementary data type, technical specifications are derived from a domain or directly maintained in the data element. Similarly, for reference data types, a reference to a global class or interface can be maintained or a reference to a predefined type can be maintained.

Figure 10.52 shows the DATA Type tab of the data element, where the technical attributes can be maintained by selecting the relevant radio button (i.e., ELEMENTARY TYPE, PREDEFINED TYPE, or REFERENCE TYPE).

![](bbox=[0.15, 0.62, 0.85, 0.83])

**Figure 10.52** Data Type Tab