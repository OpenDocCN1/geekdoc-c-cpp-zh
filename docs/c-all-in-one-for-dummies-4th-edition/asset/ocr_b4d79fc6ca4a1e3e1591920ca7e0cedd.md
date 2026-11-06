| Flag | Type | Description |
| --- | --- | --- |
| uppercase | Independent | When you write hexadecimal or scientific numbers, the various letters in the number appear as uppercase. Thus, the letters A, B, C, D, E, and F will appear in capitals in a hexadecimal number, and the E representing the exponent in scientific notation prints as a capital E. When this is not set, you get lowercase letters for hexadecimal numbers and e for the exponent in scientific notation. |

Table 2–2 shows the manipulator forms of some flags. The table shows three columns: the flag, the manipulator to turn on the flag, and the manipulator to turn off the flag.

# TABLE 2-2

### Using ANSI-Standard Manipulators and Demanipulators

| Flag | Manipulator | Demanipulator |
| --- | --- | --- |
| boolalpha | boolalpha | noboolalpha |
| showbase | showbase | noshowbase |
| showpoint | showpoint | noshowpoint |
| showpos | showpos | noshowpos |
| skipws | skipws | noskipws |
| uppercase | uppercase | nouppercase |
| fixed | fixed | scientific |
| scientific | scientific | fixed |

The scientific flag and fixed flag are opposites: fixed turns off scientific, and scientific turns off fixed. The default if you don't specify either is fixed. You don't use these flags together, such as, `cout.setf(ios_base::scientific | ios_base::fixed);`, because doing so can create some unusual and unusable results.

Six manipulators aren't in Table 2–2 because they don't have a demanipulator. Instead, they are three-way:

+   - **Bases:** `dec`, `hex`, and `oct`. Only one base can be active at a time. Activating a base automatically switches off the other bases.
+   - **Alignments:** `internal`, `left`, and `right`. Only one alignment can be active at a time. Activating an alignment automatically switches off the other alignments.