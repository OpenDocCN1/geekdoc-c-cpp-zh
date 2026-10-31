backwards-compatible change. This allows certain types of schema file restructuring.

Consider the case in which one type has been derived from another

```
```xml
<xs:simpleType name="AuthorizerId">
  <xs:restriction base="ty:UserID" />
</xs:simpleType>
```
```

Replacing a reference to the derived type AuthorizerID:

```
```xml
<xs:element name="authorizer" type="AuthorizerID">
```
```

with a reference to the base type UserID

```
```xml
<xs:element name="authorizer" type="UserID">
```
```

results in a compatible change. Note that this is true regardless of the file in which either type is defined. This technique can be used to remove redundant type definitions impacting either the provider or consumer.

# Adding an Optional Field to an XML Schema
(Conditional Future)

With the release of the XML schema 1.1 standard,³ additional types of compatible changes become possible. Under certain conditions, the addition of an optional element to a sequence is backwards compatible. This condition is that the sequence has to end with an XML any:

```
```xml
<xs:complexType name="InterestRateForTier">
  <xs:sequence>
    <xs:element name="MaxAmountForTier" type="Amount" />
    <xs:element name="InterestRate" type="Rate" />
    <xs:element name="InterestRateConfidentIndicator"
      type="boolean" />
    <xs:any minOccurs="0" maxOccurs="unbounded"
      processContents="skip" />
  </xs:sequence>
</xs:complexType>
```
```

If the any declaration occurs at the end of the sequence, then the following revised data structure is compatible with the original:

```
```xml
<xs:complexType name="InterestRateForTier">
  <xs:sequence>
    <xs:element name="MaxAmountForTier" type="Amount" />
```
```

3. XSD 1.1 became a standard on April 5, 2012.