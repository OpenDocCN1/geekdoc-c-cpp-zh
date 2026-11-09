# Chapter 8

# # Methods

In this chapter:

+   - Instance Constructors and Classes (Reference Types)
+   - 187 — Instance Constructors and Structures (Value Types)
+   - 191 — Type Constructors
+   - 194 — Operator Overload Methods
+   - 200 — Conversion Operator Methods
+   - 204 — Extension Methods
+   - 207 — Partial Methods
+   - 213

This chapter focuses on the various kinds of methods that you'll run into, including instance constructors and type constructors, as well as how to define methods to overload operators and type conversions (for implicit and explicit casting). We'll also talk about extension methods, which allow you to logically add your own instance methods to already existing types, and partial methods, which allow you to spread a type's implementation into multiple parts.

# ## Instance Constructors and Classes (Reference Types)

Constructors are special methods that allow an instance of a type to be initialized to a good state.
Constructor methods are always called .ctor (for constructor) in a method definition metadata table.
When creating an instance of a reference type, memory is allocated for the instance's data fields, the
object's overhead fields (type object pointer and sync block index) are initialized, and then the type's