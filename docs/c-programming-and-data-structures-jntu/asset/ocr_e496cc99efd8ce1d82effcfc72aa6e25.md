# Features Changed

C99 incorporates several changes to existing features. For the most part, these changes expand features or clarify their meaning. In a few cases, the changes restrict or narrow the applicability of a feature. Many such changes are small, but a few are quite important, including:

+   - Increased translation limits
+   - Extended integer types
+   - Expanded integer type promotion rules
+   - Tightening of the return statement

As it affects existing programs, the change to return has the most significant effect because it might require that code be rewritten slightly.

Throughout the remainder of this chapter, we will examine the major differences between C89 and C99.

# RESTRICT-QUALIFIED POINTERS

One of the most important innovations in C99 is the restrict type qualifier. This qualifier applies only to pointers. A pointer qualified by restrict is initially the only means by which the object it points to can be accessed. Access to the object by another pointer can occur only if the second pointer is based on the first. Thus, access to the object is restricted to expressions based on the restrict-qualified pointer. Pointers qualified by restrict are primarily used as function parameters, or to point to memory allocated via malloc(). The restrict qualifier does not change the semantics of a program. By qualifying a pointer with restrict, the compiler is better able to optimize certain types of routines by making the assumption that the restrict-qualified pointer is the sole means of access to the object. For example, if a function specifies two restrict-qualified pointer parameters, the compiler can assume that the pointers point to different (that is, non-overlapping) objects. For example, consider what has become the classic example of restrict: the memcpy() function.

In C89, it is prototyped as shown here:

```
void *memcpy(void *str1, const void *str2, size_t size);
```

The description for memcpy() states that if the objects pointed to by str1 and str2 overlap, the behaviour is undefined. Thus, memcpy() is guaranteed to work for only non-overlapping objects. In C99, restrict can be used to explicitly state in memcpy()’s prototype what C89 must explain with words.

Here is the C99 prototype for memcpy():

```
void *memcpy
(void * restrict str1, const void * restrict str2, size_t size);
```

By qualifying str1 and str2 with restrict, the prototype explicitly asserts that they point to non-overlapping objects. Because of the potential benefits that result from using restrict, C99 has added it to the prototypes for many of the library functions originally defined by C89.

# Inline

C99 adds the keyword inline, which applies to functions. By preceding a function declaration with inline, you are telling the compiler to optimize calls to the function. Typically, this means that the