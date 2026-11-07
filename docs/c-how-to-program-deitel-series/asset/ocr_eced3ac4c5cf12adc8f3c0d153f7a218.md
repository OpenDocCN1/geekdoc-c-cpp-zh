![](bbox=[0.0, 0.126, 0.093, 0.3])

+   - 18.1 Introduction
+   - 18.2 Class Templates
+   - 18.3 Function Template to Manipulate a Class-Template Specialization Object
+   - 18.4 Nontype Parameters
+   - 18.5 Default Arguments for Template Type Parameters
+   - 18.6 Overloading Function Templates
+   - 18.7 Wrap-Up
+   
+   Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# ## 18.1 Introduction

In Chapters 7, 15 and 16, you used many of the Standard Library’s *prepackaged* templa- tized containers and algorithms. Function templates (which were introduced in Chapter 6) and **class templates** enable you to conveniently specify a variety of related (overloaded) functions—called **function-template specializations**—or a variety of related classes—called **class-template specializations**, respectively. This is called **generic programming**. Function templates and class templates are like *stencils* out of which we trace shapes; function-template specializations and class-template specializations are like the separate tracings that all have the same shape, but could, for example, be drawn in different colors and textures.

In this chapter, we demonstrate how to create a custom class template and a function template that manipulates objects of this class-template specializations. We focus on the template capabilities you’ll need to build the custom templatized data structures that we present in Chapter 19.¹

# ## 18.2 Class Templates

It’s possible to understand the concept of a stack (a data structure into which we insert items *only at the top* and retrieve those items *only from the top* in *last-in, first-out order*) *independent of the type of the items* being placed in the stack. However, to *instantiate* a stack, a data type must be specified. This creates a nice opportunity for software reusability—as you already saw with the stack container adapter in Section 15.7.1. Here, we define a stack generically when use *type-specific* versions of this generic stack class.

> **Software Engineering Observation 18.1**
> 
> Class templates encourage software reusability by enabling a variety of type-specific class-template specializations to be instantiated from a single class template.

Class templates are called **parameterized types**, because they require one or more *type parameters* to specify how to customize a generic class template to form a *class-template specialization*. To produce many specializations you write only one class-template definition (as we’ll do shortly). When a particular specialization is needed, you use a concise, simple notation, and the compiler writes the specialization source code. One Stack class template, for example, could thus become the basis for creating many Stack class-template

1. Building custom templates is an advanced topic with many features that are beyond the scope of this book.