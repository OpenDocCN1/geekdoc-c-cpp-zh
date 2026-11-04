Each of these structures contains the same methods. They are shown in Table 21-2. The only difference from structure to structure is the return type of Parse(). For each structure, Parse() returns a value of the type represented by the structure. For example, for Int32, Parse() returns an int value. For UInt16, Parse() returns a ushort value. For an example that demonstrates Parse(), see Chapter 14.

In addition to the methods shown in Table 21-2, the integer structures also define the following const fields:

+   - MaxValue
+   - MinValue

For each structure, these fields contain the largest and smallest value that type of integer can hold.

All of the integer structures implement the following interfaces: IComparable, IComparable<T>, IConvertible, IFormattable, and IEquatable<T>, where T is replaced by the corresponding data type. For example, T will be replaced with int for Int32.

| Method | Meaning |
|---|---|
| public int CompareTo(object v) | Compares the numerical value of the invoking object with that of v. Returns zero if the values are equal. Returns a negative value if the invoking object has a lower value. Returns a positive value if the invoking object has a greater value. |
| public int CompareTo(type v) | Compares the numerical value of the invoking object with that of v. Returns zero if the values are equal. Returns a negative value if the invoking object has a lower value. Returns a positive value if the invoking object has a greater value. In this version of CompareTo(), type explicitly specifies the data type, such as in System.Int32.CompareTo(int v). |
| public override bool Equals(object v) | Returns true if the value of the invoking object equals the value of v. |
| public bool Equals(type v) | Returns true if the value of the invoking object equals the value of v. In this version of Equals(), type explicitly specifies the data type, such as in System.Int32.Equals(int v). |
| public override int GetHashCode() | Returns the hash code for the invoking object. |
| public TypeCode GetTypeCode() | Returns the TypeCode enumeration value for the equivalent value type. For example, for Int32, the type code is TypeCode.Int32. |
| public static retType Parse(string str) | Returns the binary equivalent of the numeric string in str. If the string does not represent a numeric value as defined by the structure type, an exception is thrown. retType is a placeholder for the actual type of data returned based on which numeric structure is used. For example, for Int32, retType will be int. |