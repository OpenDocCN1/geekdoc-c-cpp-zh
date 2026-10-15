# The EDM Types

EDM provides a basic structure to declare the schema of entities. The EDM EntityType is the basic type defined by the EDM for a top-level application concept such as e-commerce websites. The following points prove that EDM types are more based on structure than on behavior:

+   - EDM types cannot be encapsulated
+   - EDM types do not have associated methods
+   - EDM supports structural inheritance but not behavioral inheritance
+   - EDM types use simple as well as complex entity types

Now, let’s discuss the following types of EDM:

+   - Simple types
+   - Entity types
+   - Complex types

# Simple Types

In EDM, simple types are used in schemas to specify the content contained in the properties of entities. It supports attribute-constraining facets and interoperability across multiple systems. Data types can be customized according to application requirements through facets. Table 22.2 lists the simple types of EDM:

| Type | Description |
|---|---|
| Table 22.2: Simple Types of EDM | |
| Binary (EDM) | Represents fixed or variable-length binary data. |
| Boolean (EDM) | Represents the mathematical concept of two-value logics such as true or false, yes or no, and 0 or 1. |
| DateTime (EDM) | Represents date and time with values ranging from 12:00:00 midnight, January 1, 0001 A.D., to 11:59:59 P.M, December 31, 2999 A.D. The maximum precision is milliseconds. |
| Decimal (EDM) | Represents numeric values with fixed precision and scale. This type can describe a numeric value ranging from negative 10^38 + 1 to positive 10^38 -1. |
| Float (EDM) | Represents a floating point number with seven-digit precision that can represent values with approximate range of ±1.18e-38 through ±3.40e+38. |
| Double (EDM) | Represents a floating point number with 15-digit precision that can represent values with an approximate range of ±2.23e-308 to ±1.79e+308. |
| Guid (EDM) | Represents a 16-byte (128 bit) Globally Unique Identifier (GUID) value. |
| SByte (EDM) | Represents a signed 8-bit integer value. |
| Int16 (EDM) | Represents a signed 16-bit integer value. |
| Int32 (EDM) | Represents a signed 32-bit integer value. |
| Int64 (EDM) | Represents a signed 64-bit integer value. |
| Byte (EDM) | Represents an unsigned 8-bit integer value. |
| UInt16 (EDM) | Represents an unsigned 16-bit integer value. |
| UInt32 (EDM) | Represents an unsigned 32-bit integer value. |
| UInt64 (EDM) | Represents an unsigned 64-bit integer value. |
| Single (EDM) | Represents a single-precision floating-point variable as 32-bit (4-byte) floating-point number, ranging in value from -3.402823E38 to -1.401298E-45 for negative values, and 1.401298E-45 to 3.402823E38 for positive values. |
| String (EDM) | Represents fixed or variable-length character data. |