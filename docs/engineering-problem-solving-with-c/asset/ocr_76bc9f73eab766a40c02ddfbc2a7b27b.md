| alignas | alignof | and | and_eq | asm |
| :--- | :--- | :--- | :--- | :--- |
| auto | bitand | bitor | bool | break |
| case | catch | char | char16_t | char32_t |
| class | compl | const | constexpr | const_cast |
| continue | decltype | default | delete | do |
| double | dynamic_cast | else | enum | explicit |
| extern | false | float | for | friend |
| goto | if | inline | int | long |
| mutable | namespace | new | noexcept | not |
| not_eq | nullptr | operator | or | or_eq |
| private | protected | public | register | reinterpret_cast |
| return | short | signed | sizeof | static |
| static_assert | static_cast | struct | switch | template |
| this | thread_local | throw | true | try |
| typedef | typedef | typename | union | unsigned |
| using | virtual | void | volatile | wchar_t |
| while | xor | xor_eq | | |

initialized with an integer constant, will be represented in memory using the IEEE floating point representation of the integer value.

We frequently use memory snapshots to show the contents of objects both before and after a statement is executed in order to show its effect. The rules for selecting a valid identifier are as follows:

+   - an identifier must begin with an alphabetic character or the underscore character
+   - alphabetic characters in an identifier can be lowercase or uppercase letters
+   - an identifier can contain digits, but not as the first character
+   - an identifier can be of any length, but the first 31 characters of the identifier must be unique

C++ is case-sensitive, which means uppercase letters are distinguished from lowercase letters; thus Side1, SIDE1 and side1 represent three different objects. C++ also includes keywords with special meaning to the C++ compiler that cannot be used for identifiers; a complete list of keywords is given in Table 2.1.

Examples of valid identifiers are distance, x1, xSum, averageMeasurement, and initialTime. Examples of invalid identifiers are 1x (begins with a digit), switch (a keyword), $sum (contains an invalid character $), and rate% (contains an invalid character %).

An identifier name should be carefully selected so that it reflects the contents of the object, if possible, the name should also indicate the units of measurement. For example, if an object represents a temperature measurement in degrees Fahrenheit, use an identifier such as tempF or degreesF. If an object represents an angle, name it thetaRad to indicate that the angle is measured in radians or thetaDeg to indicate that the angle is measured in degrees.

![](bbox=[0.13, 0.85, 0.2, 0.9])