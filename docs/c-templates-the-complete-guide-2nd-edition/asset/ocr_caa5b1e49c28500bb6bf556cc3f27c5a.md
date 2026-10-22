To elaborate further on the possible distinctions between the two concepts, we list the following observations about traits: • Traits can be useful as *fixed traits* (i.e., without being passed through template parameters).
• Traits parameters usually have very natural default values (which are rarely overridden, or simply cannot be overridden).
• Traits parameters tend to depend tightly on one or more main parameters.
• Traits mostly combine types and constants rather than member functions.
• Traits tend to be collected in traits *templates*.
For policy classes, we make the following observations:
• Policy classes don’t contribute much if they aren’t passed as template parameters.
• Policy parameters need not have default values and are often specified explicitly (although many generic components are configured with commonly used default policies).
• Policy parameters are mostly orthogonal to other parameters of a template.
• Policy classes mostly combine member functions.
• Policies can be collected in plain classes or in class templates.
However, there is certainly an indistinct line between both terms. For example, the character traits of the C++ standard library also define functional behavior such as comparing, moving, and finding characters. And by replacing these traits, we can define string classes that behave in a case-insensitive manner (see Section 13.2.15 in [JosuttisStdLib]) while keeping the same character type. Thus, although they are called *traits*, they have some properties associated with policies.

# 19.2.2 Member Templates versus Template Template Parameters

To implement an accumulation policy, we chose to express SumPolicy and MultPolicy as ordinary classes with a member template. An alternative consists of designing the policy class interface using class templates, which are then used as template template arguments (see Section 5.7 on page 83 and Section 12.2.3 on page 187). For example, we could rewrite SumPolicy as a template: Click here to view code image

```
traits/sumpolicy2.hpp
```