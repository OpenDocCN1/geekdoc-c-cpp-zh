For example, if you performed a screen enhancement for Transaction ME21N to capture additional data while creating a purchase order, then the corresponding `Create( )` BAPI for a business object type purchase order can be enhanced to process this additional data using the extension structures. The extension structures are based on the type `BAPIPAREX`.

The following conventions should be followed for *parameters*:

+   - Wherever possible, optional parameters should be used to avoid incompatible changes in the future and provide stability to the interface.
+   - Related parameters should be grouped into a structure instead of using too many scalar parameters.
+   - The parameter names should be as meaningful as possible. Avoid using technical names, such as *table names*, or abbreviations, such as *flag*.
+   - The parameter names should be in English and a maximum of thirty characters.
+   - For ISO-relevant fields such as country, language, unit of measure, and so on, additional fields for ISO codes should be provided. For example, if you have a language field `LANGU`, then an additional field for the ISO code should be provided as `LANGU_ISO`.
+   - A quantity field must accompany a unit of measure field. Similarly, a currency field must accompany a currency identifier.

# Defining the Data Structure in the ABAP Dictionary

Once the parameter interface is identified, the required data structures should be defined in ABAP Data Dictionary. This includes defining the required structure, data elements, domains, and so on. We discussed defining these data structures in [Chapter 10](#chapter-10).

When defining the data structures in ABAP Data Dictionary for the BAPI interface, certain conventions should be followed:

+   - The name of the structure should start with `(namespace)BAPI_`. For example, `ZBAPI_`. If the parameter of a BAPI is a structure, it can be referred directly to this structure in ABAP Data Dictionary. However, if the parameter is an individual field, then it should be referred to the component of the structure.
+   - You should create separate data structures for BAPIs and not use the existing structures used for the applications, because when the BAPI is released, the