```
REPORT ZDEMO_EXAMPLES.
TYPES: ty_type TYPE p DECIMALS 2.
DATA: v_data TYPE ty_type.
      r_typedescr TYPE REF TO cl_abap_typedescr.
START-OF-SELECTION.
r_typedescr = cl_abap_typedescr->describe_by_data( v_data ).

WRITE: / 'Kind:',    r_typedescr->type_kind.
WRITE: / 'Length:',  r_typedescr->length.
WRITE: / 'Decimals:', r_typedescr->decimals.
```

# Listing 16.25  Querying Type Information

In Listing 16.25, we've defined a R_TYPEDESCR type object as an instance of the type class CL_ABAP_TYPEDESCR. The type object is instantiated when the DESCRIBE_BY_DATA static method of the type class is called. To this static method, we're passing the data object for which the type information is required.

Once the type object is instantiated with the type information, we can access its attributes to determine the type information of the data object. The type object also contains constants that can be used in an IF or CASE structure to compare the TYPE_KIND attribute.

# 16.3.2  Runtime Type Creation

As discussed in the previous section, type objects are created using RTTI methods of RTTS; these type objects can be used to create new types using the RTTC methods of RTTS. The RTTC methods allow you to dynamically create data types that can be used to define data objects dynamically.

For example, say you want to dynamically create a structure on the fly and use it in a SELECT statement. You'll only know the fields of the structure at runtime. In such a situation, you use the RTTC methods to define a data type and use to dynamically create the data object. The GET factory method of the CL_ABAP_STRUCTDESCR, CL_ABAP_TABLEDESCR, and CL_ABAP_REFDESCR classes allows you to create a type object.

The required information to create the type object is passed to the factory method of these classes. For example, the component details are passed to the factory method of the CL_ABAP_STRUCTDESCR class to create the type object for structure. Similarly, the structure type object is passed to the factory method of the CL_ABAP_TABLEDESCR class to create the table type object. Listing 16.26 shows how