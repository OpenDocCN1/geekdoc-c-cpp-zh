# Output

The value of pi is 3.14.

# 2.5 Identifier

# Concept

+   - Identifiers are arbitrary names in C# program. Identifiers are names used to identify code elements.
+   - The term identifier is usually used for variable names, arrays, name of class, method names, labels, namespace and interface etc.

# Explanation

3. Following are some rules for defining identifiers -

+   - Identifiers can have alphabets, underscore and digits characters provided First character must be an alphabet or underscore. It cannot have more than 511 characters.
+   - It has to be declared before it is referred.
+   - It must not contain any embedded space or symbol such as? - + ! @ # % ^ & * ( ) [] { } ; : . " / and \. However, an underscore ( _ ) can be used.
+   - It cannot have two consecutive underscores in its name because such identifiers are used for the implementation
+   - White spaces are not allowed in identifier.
+   - Identifiers must not start with a Digit.
+   - For identifiers Upper case and lower case letters are distinct. That is, good, GOOD & Good are different identifiers than with each other. This indicates that C# is case sensitive.
+   - Keywords cannot be used as identifier names. If the identifier is a keyword, it must be prefixed with '@'. An identifier prefixed with "@" is called a verbatim identifier. Although prefixing "@" allows for the use of keywords, which helps in interfacing with other programming languages, it is not a recommended practice.
+   - More than one identifier with the same name cannot be declared within a single scope

# Example

The following names are valid identifiers in C#

+   - INDIA
+   - salary
+   - I_ndia
+   - HelloWorld