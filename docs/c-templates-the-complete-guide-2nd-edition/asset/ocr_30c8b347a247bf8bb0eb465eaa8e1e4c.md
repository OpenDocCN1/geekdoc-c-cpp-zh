class template is then instantiated (and compiled) for these types.

+   - For class templates, only those member functions that are called are instantiated.
+   - You can specialize class templates for certain types.
+   - You can partially specialize class templates for certain types.
+   - Since C++17, class template arguments can automatically be deduced from constructors.
+   - You can define aggregate class templates.
+   - Call parameters of a template type decay if declared to be called by value.
+   - Templates can only be declared and defined in global/namespace scope or inside class declarations.

1 C++17 introduced class argument template deduction, which allows skipping template arguments if they can be derived from the constructor. This will be discussed in Section 2.9 on page 40.

2 It is a templated entity, see Section 12.1 on page 181.

3 Using the word typedef instead of “type definition” in intentional. The keyword typedef was originally meant to suggest “type definition.” However, in C++, “type definition” really means something else (e.g., the definition of a class or enumeration type). Instead, a typedef should just be thought of as an alternative name (an “alias”) for an existing type, which can be done by a typedef.

4 Alias templates are sometimes (incorrectly) referred to as typedef templates because they fulfill the same role that a typedef would if it could be made into a template.

5 The typename is necessary here because the member is a type. See Section 5.1 on page 67 for details.

6 Even worse, there is a vector constructor taking one integral argument as initial size, so that for a stack with the initial value 5, the vector would get an initial size of five elements when : elems(elem) is used.