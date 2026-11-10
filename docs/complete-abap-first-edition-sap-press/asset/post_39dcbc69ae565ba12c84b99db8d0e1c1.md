
![](img/5f2e77efd858ed75fdad8c2a2aa83c8f_680_0.png)

**Figure 16.3** Data Reference Variable in Debug Mode

## 16.2.2 Getting Data References

The `GET REFERENCE OF` statement is used to obtain a reference to an existing data object. You can obtain a reference to an existing data object, an assigned field symbol, or a dereferenced data reference variable.

[Listing 16.18](#listing-16-18) shows how to obtain a data reference using the `GET REFERENCE OF` statement from a data object, field symbol, or dereferenced reference variable.

```abap
DATA v_matnr TYPE matnr VALUE '100'.
DATA dref TYPE REF TO matnr.
DATA dref1 TYPE REF TO matnr.
FIELD-SYMBOLS <fs> TYPE matnr.
ASSIGN v_matnr TO <fs>.
*Getting reference from data object
GET REFERENCE OF v_matnr INTO dref.
*Getting reference from dereferenced reference variable
GET REFERENCE OF dref->* INTO dref1.
*Getting reference from field symbol
GET REFERENCE OF <fs> INTO dref1.
WRITE dref->*.
```

**Listing 16.18** Getting Data Object Reference

Once the data object reference is obtained, the reference variable should be dereferenced to access the contents of the referenced data object. For example, in [Listing 16.18](#listing-16-18), we’re dereferencing the reference variable using the `->*` dereference selector to access the contents of the referenced data object with the WRITE statement.

Once the reference variable is dereferenced, the reference variable can be used to perform any actions or use any statements that are possible with the referenced data object. You can dereference the data reference variable directly only if it's fully typed. If the reference variable is generically typed, then it should be assigned to a field symbol to access the contents of the referenced data object.

Listing 16.19 shows an example using generic reference variables.

```abap
DATA v_matnr TYPE matnr VALUE '100'.
DATA dref TYPE REF TO data.
FIELD-SYMBOLS <fs> TYPE any.

GET REFERENCE OF v_matnr INTO dref.
ASSIGN dref->* TO <fs>.
* WRITE dref->*. " Results in syntax error
WRITE <fs>.
```

Listing 16.19 Dereferencing Generic Type

In Listing 16.19, the DREF reference variable is declared as a generic type. The reference of data object V_MATNR is obtained using the GET REFERENCE statement. However, because the DREF reference variable is a generic type, we can't access the contents of V_MATNR by directly dereferencing the reference variable as we did in the WRITE statement in Listing 16.18; in fact, dereferencing a generic type results in a syntax error.

To dereference the generic type, we assign it to a field symbol as shown in Listing 16.19. If the reference variable has an empty reference, then the field symbol will not be assigned. You can check if the field symbol is assigned before accessing it to avoid an untreatable exception.

## 16.2.3 Anonymous Data Objects

Anonymous data objects are used when the data type is unknown statically. When we define data objects using the DATA statement, all the data objects are created by the runtime environment when the program starts. All these data objects can be accessed in the program statically using the name of the data object. These are called named data objects.

Anonymous data objects are created on demand in the program as required and can be assigned a suitable type per requirements. You use the `CREATE DATA` statement to instantiate an anonymous data object with the following syntax:

```abap
CREATE DATA dref TYPE|LIKE dtype.
```

The `CREATE DATA` statement creates an anonymous data object and assigns the reference of the data object to the reference variable. Anonymous data objects can't be accessed directly by their names. The data object needs to be dereferenced to access its contents.

[Listing 16.20](#) shows an example using an anonymous data object.

```abap
FIELD-SYMBOLS <fs> TYPE DATA.
DATA dref TYPE REF TO DATA.
CREATE DATA dref TYPE i.
ASSIGN dref->* TO <fs>.
<fs> = 5.
```

**Listing 16.20** Anonymous Data Object

The data type can be specified dynamically using a field in parenthesis—for example, `CREATE DATA dref TYPE (name)`. Here, `name` is a data object that contains the data type.

With the release of SAP NetWeaver 7.4, a new instantiation operation, `NEW`, has been introduced to instantiate both data references and object references in lieu of the `CREATE` statement. The `NEW` statement, as shown in [Listing 16.21](#), takes its cue from other programming languages, such as Java.

```abap
FIELD-SYMBOLS <fs> TYPE DATA.
DATA dref TYPE REF TO data.
dref = NEW i( 5 ).
ASSIGN dref->* TO <fs>.
```

**Listing 16.21** Using NEW Instantiation Operator

Similarly to accessing reference objects, you can access the components of a data reference using the `->` selector—for example, `DREF->COMP`. If no `TYPE` specification is provided with the `CREATE DATA` statement, the anonymous data object is created as a static type of the data reference variable.

[Listing 16.22](#) shows example code to access components of the anonymous data object.

```abap
TYPES: BEGIN OF ty_mara,
         matnr TYPE matnr,
         mtart TYPE mtart,
       END OF ty_mara.
DATA dref TYPE REF TO ty_mara.
CREATE DATA dref.
dref->matnr = '100'.
```

**Listing 16.22** Accessing Components of Anonymous Data Objects

You can use the IS BOUND statement to check if the data reference variable contains a valid reference and is dereferenceable—for example, IF dref IS BOUND.

## 16.2.4 Assignment between Reference Variables

As with object references, you can perform assignments between data references. When a data reference is assigned, the target reference variable will point to the same data object as the source reference variable.

A reference variable can be assigned only to another reference variable. In other words, you can't assign a reference variable to a data object or a reference object and vice versa.

Like object references, data references also support upcasting and downcasting. When assigning a reference variable, if the static type of the source reference variable is similar to or more special than the static type of the target reference variable, then an upcast is performed. You can use the `=` assignment operator or the `MOVE` statement to perform the assignment.

An upcast is performed when the target reference variable is a generic type and the source reference variable is fully typed, as shown in Listing 16.23.

```abap
TYPES: BEGIN OF ty_mara,
         matnr TYPE matnr,
         mtart TYPE mtart,
       END OF ty_mara.
DATA : dref TYPE REF TO ty_mara, " Fully Typed
       dref1 TYPE REF TO DATA. " Generic type
CREATE DATA dref.
dref1 = dref. " Upcast
```

**Listing 16.23** Upcast

If the static type of the source reference variable is more general than the static type of the target reference variable, it leads to a downcast. The assignment can only be validated at runtime, because the type of the source reference variable will be known only at runtime.

For this assignment, the syntax checker can't validate statically and will throw a syntax error if the `=` assignment operator or the `MOVE` statement is used for the assignment.

For such assignments, we have to use the `?=` casting operator or the `MOVE ?TO` statement. An upcast is performed if the source reference variable is of a generic type and the target reference variable is fully typed.

Listing 16.24 shows an example of a downcast.

```abap
TYPES: BEGIN OF ty_mara,
         matnr TYPE matnr,
         mtart TYPE mtart,
       END OF ty_mara.
DATA : s_mara TYPE ty_mara,
       dref TYPE REF TO ty_mara, " Fully Typed
       dref1 TYPE REF TO DATA. " Generic type
CREATE DATA dref.
GET REFERENCE OF s_mara INTO dref1.
TRY.
  dref ?= dref1. " Down Cast
CATCH cx_sy_move_cast_error.
ENDTRY.
```

**Listing 16.24** Downcast

## 16.3 Runtime Type Services

ABAP *Runtime Type Services* (RTTS) is an object-oriented framework that consists of the following elements:

- **Runtime Type Information (RTTI)**  
  Using RTTI, we can determine the type information about data objects or instances of classes at runtime during program execution.
- **Runtime Type Creation (RTTC)**  
  RTTC allows us to define new data types during the program execution.

The RTTS framework implements a hierarchy of classes, as shown in Figure 16.4, via which we can determine the type information of data objects and define new
