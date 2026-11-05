The following operators can be used on values of enum types: ==, !=, <, >, <=, >= (§7.10.5), binary + (§7.8.4), binary - (§7.8.5), ^, &, | (§7.11.2), ~ (§7.7.4), and ++ and -- (§7.6.9 and §7.7.5).

> JON SKEET Some of these operators really make sense just for enums decorated with [Flags], but the language does not enforce this limitation in any sense.

Every enum type automatically derives from the class System.Enum (which, in turn, derives from System.ValueType and object). Thus inherited methods and properties of this class can be used on values of an enum type.