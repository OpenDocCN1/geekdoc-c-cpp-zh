# # 18 Reflection, Attributes, and Dynamic Programming

Attributes are a means of inserting additional metadata into an assembly and associating the metadata with a programming construct such as a class, method, or property. This chapter investigates the details surrounding attributes that are built into the framework and describes how to define custom attributes. To take advantage of custom attributes, it is necessary to identify them. This is handled through reflection.

This chapter begins with a look at reflection, including how you can use it to dynamically bind at execution time based on member invocation (or metadata) at compile time. Reflection is frequently leveraged within tools such as a code generator. In addition, reflection is used at execution time when the call target is unknown.

The chapter ends with a discussion of dynamic programming,¹ a feature that greatly simplifies working with data that is dynamic and requires execution-time rather than compile-time binding.

# Reflection

Using reflection, it is possible to do the following:

+   1. Added in C# 4.0.