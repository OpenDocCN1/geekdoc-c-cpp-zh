© ISO/IEC 2011 – All rights reserved

ISO/IEC 9899:2011 (E)

# Annex F

# (normative)

# IEC 60559 floating-point arithmetic

# F.1 Introduction

+   - This annex specifies C language support for the IEC 60559 floating-point standard. The IEC 60559 floating-point standard is specifically Binary floating-point arithmetic for microprocessor systems, second edition (IEC 60559:1989), previously designated IEC:559:1989 and as IEEE Standard for Binary Floating-Point Arithmetic (ANSI/IEEE 754–1985). IEEE Standard for Radix-Independent Floating-Point Arithmetic (ANSI/IEEE 854–1987) generalizes the binary standard to remove dependencies on word length. IEC 60559 generally refers to the floating-point standard, as in IEC 60559 operation, IEC 60559 format. An implementation that defines __STDC_IEC_559__ shall conform to the specifications in this annex. Where a binding between the C language and IEC 60559-specified is adopted by reference, unless stated otherwise. Since negative and positive infinity are representable in IEC 60559 formats, all real numbers lie within the range of representable values.

# F.2 Types

+   - The float type matches the IEC 60559 single format.
- The double type matches the IEC 60559 double format.
- The long double type matches an IEC 60559 extended format, a non-IEC 60559 extended format, else the IEC 60559 double format.

Any non-IEC 60559 extended format used for the long double type shall have precision than IEC 60559 double and at least the range of IEC 60559 double.

> 356 Implementations that do not define __STDC_IEC_559__ are not required to conform to these specifications.

> 357 “Extended” is IEC 60559’s double-extended data. Extended refers to both the double and quad 128-bit IEC 60559 formats.

> 358 A non-IEC 60559 long double type is required to provide infinity and NaNs, as its values include all values.

§F.2 IEC floating-point arithmetic

507