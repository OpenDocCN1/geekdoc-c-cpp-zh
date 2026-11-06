
## Summary

### Section 18.1 Introduction

- Templates enable us to specify a range of related (overloaded) functions—called **function-template specializations** (p. **785**)—or a range of related classes—called **class-template specializations** (p. **785**).

### Section 18.2 Class Templates

- Class templates provide the means for describing a class generically and for instantiating classes that are type-specific versions of this generic class.
- Class templates are called **parameterized types** (p. 785); they require type parameters to specify how to customize a generic class template to form a specific class-template specialization.
- To use class-template specializations you write one class template. When you need a new type-specific class, the compiler writes the source code for the class-template specialization.
- A **class-template definition** (p. 785) looks like a conventional class definition, but it’s preceded by `template<typename T>` (or `template<class T>`) to indicate this is a class-template definition. `T` is a type parameter that acts as a placeholder for the type of the class to create. The type `T` is mentioned throughout the class definition and member-function definitions as a generic type name.
- The names of template parameters must be unique inside a template definition.
- Member-function definitions outside a class template each begin with the same `template` declaration as their class. Then, each function definition resembles a conventional function definition, except that the generic data in the class always is listed generically as type parameter `T`. The binary scope-resolution operator is used with the class-template name to tie each member-function definition to the class template’s scope.

### Section 18.4 Nontype Parameters

- It’s possible to use **nontype parameters** (p. 792) in a class or function template declaration.

### Section 18.5 Default Arguments for Template Type Parameters

- You can specify a **default type argument** (p. 792) for a type parameter in the type-parameter list.

### Section 18.6 Overloading Function Templates

- A function template may be overloaded in several ways. We can provide other function templates that specify the same function name but different function parameters. A function template can also be overloaded by providing other nontemplate functions with the same function name, but different function parameters. If both the template and non-template versions match a call, the non-template version will be used.

## Self-Review Exercises

- **18.1** State which of the following are *true* and which are *false*. If *false*, explain why.
  - **A.** Keywords `typename` and `class` as used with a template type parameter specifically mean “any user-defined class type.”
  - **B.** A function template can be overloaded by another function template with the same function name.
  - **C.** Template parameter names among template definitions must be unique.
  - **D.** Each member-function definition outside its corresponding class template definition must begin with `template` and the same template parameters as its class template.

- **18.2** Fill in the blanks in each of the following:
  - **A.** Templates enable us to specify, with a single code segment, an entire range of related functions called ________, or an entire range of related classes called ________.
  - **B.** All template definitions begin with the keyword ________, followed by a list of template parameters enclosed in ________.
  - **C.** The related functions generated from a function template all have the same name, so the compiler uses ________ resolution to invoke the proper function.
  - **D.** Class templates also are called ____ types.
  - **E.** The ____ operator is used with a class-template name to tie each member-function definition to the class template’s scope.

## Exercises

- **18.3** (*Operator Overloads in Templates*) Write a simple function template for predicate function `isEqualTo` that compares its two arguments of the same type with the equality operator (`==`) and returns `true` if they are equal and `false` otherwise. Use this function template in a program that calls `isEqualTo` only with a variety of fundamental types. Now write a separate version of the program that calls `isEqualTo` with a user-defined class type, but does not overload the equality operator. What happens when you attempt to run this program? Now overload the equality operator (with the operator function) `operator==`. Now what happens when you attempt to run this program?
- **18.4** (*Array* Class Template) Reimplement class `Array` from Figs. 10.10–10.11 as a class template. Exercise each of the new `Array` class template’s capabilities in a program.
- **18.5** Distinguish between the terms “function template” and “function-template specialization.”
- **18.6** Explain which is more like a stencil—a class template or a class-template specialization?
- **18.7** What’s the relationship between function templates and overloading?
- **18.8** The compiler performs a matching process to determine which function-template specialization to call when a function is invoked. Under what circumstances does an attempt to make a match result in a compile error?
- **18.9** Why is it appropriate to refer to a class template as a parameterized type?
- **18.10** Explain why a C++ program would use the statement

  ```
  Array<Employee> workerList{10};
  ```

- **18.11** Review your answer to Exercise 18.10. Explain why a C++ program might use the statement

  ```
  Array<Employee> workerList;
  ```

- **18.12** Explain the use of the following notation in a C++ program:

  ```
  template <typename T> Array<T>::Array(int s)
  ```

- **18.13** Why might you use a nontype parameter with a class template for a container such as an array or stack?
- **18.14** (*GradeBook Class Template*) Reimplement class `GradeBook` from **Section 7.9** as a class template with two nontype template parameters that represent the number of students and the number of tests (as described in **Section 18.4**). Test multiple instances of the `GradeBook` class template with different numbers of students and exams.

## Answers to Self-Review Exercises

- **18.1**
  - **A.** False. Keywords `typename` and `class` in this context also allow for a type parameter of a fundamental type.
  - **B.** True.
  - **C.** False. Template parameter names among function templates need not be unique.
  - **D.** True.

- **18.2**
  - **A.** function-template specializations, class-template specializations.
  - **B.** `template`, angle brackets (`<` and `>`).
  - **C.** overload.
  - **D.** parameterized.
  - **E.** scope resolution.

## 19 Custom Templatized Data Structures

### Objectives

In this chapter you’ll:

- Form linked data structures using pointers, self-referential classes and recursion.
- Create and manipulate dynamic data structures such as linked lists, queues, stacks and binary trees.
- Use binary search trees for high-speed searching and sorting.
- Learn important applications of linked data structures.
- Create reusable data structures with class templates, inheritance and composition.
- Have the opportunity to try many challenging data-structures exercises, including the Building Your Own Compiler project.

### Outline

- **19.1 Introduction**
  - **19.1.1 Always Prefer the Standard Library’s Containers, Iterators and Algorithms, if Possible**
  - **19.1.2 Special Section: Building Your Own Compiler**
- **19.2 Self-Referential Classes**
- **19.3 Linked Lists**
  - **19.3.1 Testing Our Linked List Implementation**
  - **19.3.2 Class Template `ListNode`**
  - **19.3.3 Class Template `List`**
  - **19.3.4 Member Function `insertAtFront`**
  - **19.3.5 Member Function `insertAtBack`**
  - **19.3.6 Member Function `removeFromFront`**
  - **19.3.7 Member Function `removeFromBack`**
  - **19.3.8 Member Function `print`**
  - **19.3.9 Circular Linked Lists and Doubly Linked Lists**
- **19.4 Stacks**
  - **19.4.1 Taking Advantage of the Relationship Between `Stack` and `List`**
  - **19.4.2 Implementing a Class Template `Stack` Class by Inheriting from `List`**
  - **19.4.3 Dependent Names in Class Templates**
