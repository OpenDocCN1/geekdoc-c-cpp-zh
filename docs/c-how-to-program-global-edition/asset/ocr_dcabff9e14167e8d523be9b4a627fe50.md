+   Outline
+   23.1 Introduction
+   23.5 Default Arguments for Template Type Parameters
+   23.2 Class Templates
+   23.6 Overloading Function Templates
+   23.3 Function Template to Manipulate a Class-Template Specialization Object
+   23.7 Wrap-Up
+   23.4 Nontype Parameters
+   Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# ### 23.1 Introduction

The C++ Standard Library contains many prepackaged templatized data structures and algorithms. Function templates (which were introduced in Chapter 15) and class templates enable you to conveniently specify a variety of related (overloaded) functions—called function-template specializations—or a variety of related classes—called class-template specializations, respectively. This is called generic programming. Function templates and class templates are like *stencils* out of which we trace shapes; function-template specializations and class-template specializations are like the separate tracings that all have the same shape, but could, for example, be drawn in different colors and textures. In this chapter, we demonstrate how to create a custom class template and a function template that manipulates objects of our class-template specializations.

# ### 23.2 Class Templates

It's possible to *understand* the concept of a stack (a data structure into which we insert items only at the top and retrieve those items only from the top in last-in, first-out order) independent of the type of the items being placed in the stack. However, to instantiate a stack, a data type must be specified. This creates a nice opportunity for software reusability. Here, we define a stack *generically* then use *type-specific* versions of this generic stack class.

> **Software Engineering Observation 23.1**
> *Class templates encourage software reusability by enabling a variety of type-specific class-template specializations to be instantiated from a single class template.*

Class templates are called parameterized types, because they require one or more *type parameters* to specify how to customize a generic class template to form a *class-template specialization*. To produce many specializations you write only one class-template definition (as we'll do shortly). When a particular specialization is needed, you use a concise, simple notation, and the compiler writes the specialization source code. One Stack class template, for example, could thus become the basis for creating many Stack class-template specializations (such as "Stack of doubles," "Stack of ints," "Stack of Employees," "Stack of Bills," etc.) used in a program.