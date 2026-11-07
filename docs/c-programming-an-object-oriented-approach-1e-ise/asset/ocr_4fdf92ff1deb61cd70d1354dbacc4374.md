| Table 16.19 | Manipulators using formatting fields |  |  |  |
|---|---|---|---|---|
| Flag | Manipulator | Effect | In | Out |
| basefield | dec | Show integers in decimal. | ✓ | ✓ |
|  | hex | Show integers in hexadecimal. | ✓ | ✓ |
|  | oct | Show integers in octal. | ✓ | ✓ |
| floatfield | fixed | Show type in fixed format. |  | ✓ |
|  | scientific | Show type in scientific format. |  | ✓ |
| adjustfield | right | Right justify the data in the field. |  | ✓ |
|  | left | Left justify the data in the field. |  | ✓ |
|  | internal | Justify data internally in the field. |  | ✓ |

# Manipulators Related to Formatting Variables

In Table 16.17 we mentioned three sets of member functions to set variable fields. We have three manipulators that look like a function with parameters (Table 16.20).

# Manipulator Not Related to Flags or Fields

There are four manipulators that are not related to any flag or field. They perform specific actions on the stream (Table 16.21).

We repeat the program but use manipulators instead of formatting flags, fields, and variables to achieve the same goal as shown in Program 16.23. Note that we need to include the header file `<iomanip>` for manipulators related to formatting variables.

# 16.5.3  Manipulators Definition

If we want to create new manipulators, we must first learn how predefined manipulators are defined.

| Table 16.20 | Manipulators using variable fields |  |  |  |
|---|---|---|---|---|
| Variables | Manipulator | Effect | In | Out |
| width | setw (n) | Set n character as the field. | ✓ | ✓ |
| precision | setprecision (n) | Set n characters for precision. |  | ✓ |
| fill | setfill (c) | Use c as the fill character. | ✓ | ✓ |

| Table 16.21 | Manipulators using no flags or fields |  |  |
|---|---|---|---|
| Manipulator | Effect | In | Out |
| ws | Extract white spaces. | ✓ |  |
| endl | Insert new line and flush the buffer. |  | ✓ |
| ends | Insert end of string character. |  | ✓ |
| flush | Flush stream buffer. |  | ✓ |