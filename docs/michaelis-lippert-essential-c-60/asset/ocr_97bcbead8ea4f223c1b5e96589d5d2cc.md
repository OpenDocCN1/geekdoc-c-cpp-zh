0.09999999999999999 or 0.10000000000000001 or some other number very close to 0.1. Similarly, setting a variable to a large number such as Avogadro’s number, 6.02 × 10²³, could lead to a representation error of approximately 10⁸, which after all is a tiny fraction of that number. The accuracy of a floating-point number is in proportion to the magnitude of the number it represents. A floating-point number is precise to a certain number of significant digits, not by a fixed value such as ±0.01.

C# supports the two binary floating-point number types listed in Table 2.2.

**TABLE 2.2: Floating-Point Types**

| Type | Size | Range (Inclusive) | BCL Name | Significant Digits | Literal Suffix |
|---|---|---|---|---|---|
| `float` | 32 bits | ±1.5 × 10⁻⁴⁵ to ±3.4 × 10³⁸ | `System.Single` | 7 | F or f |
| `double` | 64 bits | ±5.0 × 10⁻³²⁴ to ±1.7 × 10³⁰⁸ | `System.Double` | 15–16 | — |

Binary numbers appear as base 10 (denary) numbers for human readability. The number of bits (binary digits) converts to 15 decimal digits, with a remainder that contributes to a sixteenth decimal digit as expressed in Table 2.2. Specifically, numbers between 1.7 × 10³⁰⁷ and less than 1 × 10³⁰⁸ have only 15 significant digits. However, numbers ranging from 1 × 10³⁰⁸ to 1.7 × 10³⁰⁸ will have 16 significant digits. A similar range of significant digits occurs with the decimal type as well.

# Decimal Type

C# also provides a decimal floating-point type with 128-bit precision (see Table 2.3). This type is suitable for financial calculations.

**TABLE 2.3: decimal Type**

| Type | Size | Range (Inclusive) | BCL Name | Significant Digits | Literal Suffix |
|---|---|---|---|---|---|
| `decimal` | 128 bits | 1.0 × 10⁻²⁸ to approximately 7.9 × 10²⁸ | `System.Decimal` | 28–29 | M or m |