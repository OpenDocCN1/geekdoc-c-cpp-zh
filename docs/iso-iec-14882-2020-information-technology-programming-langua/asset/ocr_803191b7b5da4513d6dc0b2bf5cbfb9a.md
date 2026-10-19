# 7.3.6 Qualification conversions [conv.qual]

1 A cv-decomposition of a type T is a sequence of cv_i and P_i such that T is “cv0 P0 cv1 P1 ⋯ cvn−1 Pn−1 cvn U” for n ≥ 0, where each cv_i is a set of cv-qualifiers (6.8.4), and each P_i is “pointer to” (9.3.4.2), “pointer to member of class C_i of type” (9.3.4.4), “array of N_i”, or “array of unknown bound of” (9.3.4.5). If P_i designates an array, the cv-qualifiers cv_{i+1} on the element type are also taken as the cv-qualifiers cv_i of the array.

> [Example 1: The type denoted by the type-id const int ** has three cv-decompositions, taking U as “int”, as “pointer to const int”, and as “pointer to pointer to const int”. — end example]

The n-tuple of cv-qualifiers after the first one in the longest cv-decomposition of T, that is, cv1, cv2, …, cvn, is called the cv-qualification signature of T.

2 Two types T1 and T2 are similar if they have cv-decompositions with the same n such that corresponding P_i components are either the same or one is “array of N_i” and the other is “array of unknown bound of”, and the types denoted by U are the same.

3 The cv-combined type of two types T1 and T2 is the type T3 similar to T1 whose cv-decomposition is such that:

+   (3.1) — for every i > 0, cv_i^3 is the union of cv_i^1 and cv_i^2,
+   (3.2) — if either P_i^1 or P_i^2 is “array of unknown bound of”, P_i^3 is “array of unknown bound of”, otherwise it is P_i^1, and
+   (3.3) — if the resulting cv_i^3 is different from cv_i^1 or cv_i^2, or the resulting P_i^3 is different from P_i^1 or P_i^2, then const is added to every cv_k^3 for 0 < k < i,

where cv_i^j and P_i^j are the components of the cv-decomposition of Tj. A prvalue of type T1 can be converted to type T2 if the cv-combined type of T1 and T2 is T2.

> [Note 1: If a program were able to assign a pointer of type T** to a pointer of type const T** (that is, if line #1 below were allowed), it would be possible for a const object to be inadvertently modified (as is done on line #2). For example,]

```
int main() {
    const char c = 'c';
    char* pc;
    const char** pcc = &pc;      // #1: not allowed
    *pcc = &c;
    *pc = 'C';                  // #2: modifies a const object
}
```

> — end note

> [Note 2: Given similar types T1 and T2, this construction ensures that both can be converted to the cv-combined type of T1 and T2. — end note]

> 4 [Note 3: A prvalue of type “pointer to cv1 T” can be converted to a prvalue of type “pointer to cv2 T” if “cv2 T” is more cv-qualified than “cv1 T”. A prvalue of type “pointer to member of X of type cv1 T” can be converted to a prvalue of type “pointer to member of X of type cv2 T” if “cv2 T” is more cv-qualified than “cv1 T”. — end note]

> 5 [Note 4: Function types (including those used in pointer-to-member-function types) are never cv-qualified (9.3.4.6). — end note]

# 7.3.7 Integral promotions [conv.prom]

1 A prvalue of an integer type other than bool, char16_t, char32_t, or wchar_t whose integer conversion rank (6.8.5) is less than the rank of int can be converted to a prvalue of type int if int can represent all the values of the source type; otherwise, the source prvalue can be converted to a prvalue of type unsigned int.

2 A prvalue of type char16_t, char32_t, or wchar_t (6.8.2) can be converted to a prvalue of the first of the following types that can represent all the values of its underlying type: int, unsigned int, long int, unsigned long int, long long int, or unsigned long long int. If none of the types in that list can represent all the values of its underlying type, a prvalue of type char16_t, char32_t, or wchar_t can be converted to a prvalue of its underlying type.