If you allocate objects of a built-in type using **new**, they will not be initialized unless you specify an initializer. If you allocate objects of a class with a constructor using **new**, a constructor is called; the default constructor is called unless you specify an initializer (§17.4.4).  
A **delete** invokes the destructor, if any, for its operand. Note that a destructor may be virtual (§A.12.3.1).

# A.5.7 Casts

There are four type-conversion operators:

|  
Type-conversion operators |  
|:-------------------------------------------------------------------------|:-------------------------------------------------------------------------|
| x=dynamic_cast<D*>(p) | Try to convert **p** into a **D*** (may return **0**). |
| x=dynamic_cast<D&>(p) | Try to convert **p** into a **D&** (may throw **bad_cast**). |
| x=static_cast<T>(v) | Convert **v** into a **T** if a **T** can be converted into **v**'s type. |
| x=reinterpret_cast<T>(v) | Convert **v** into a **T** represented by the same bit pattern. |
| x=const_cast<T>(v) | Convert **v** into a **T** by adding or subtracting **const**. |
| x=(Tv) | C-style cast: do any old cast. |
| x=T(v) | Functional cast: do any old cast. |
| x=T{v} | Construct a **T** from **v** (no narrowing will be done). |

The dynamic cast is typically used for class hierarchy navigation where **p** is a pointer to a base class and **D** is derived from that base. It returns **0** if **v** is not a **D***.  
If you want **dynamic_cast** to throw an exception (**bad_cast**) instead of returning **0**, cast to a reference instead of to a pointer. The dynamic cast is the only cast that relies on run-time checking.

Static cast is used for “reasonably well-behaved conversions,” that is, where **v** could have been the result of an implicit conversion from a **T**; see §17.8.

Reinterpret cast is used for reinterpreting a bit pattern. It is not guaranteed to be portable. In fact, it is best to assume that every use of **reinterpret_cast** is non-portable. A typical example is an **int**-to-pointer conversion to get a machine address into a program; see §17.8 and §25.4.1.

The C-style and functional casts can perform any conversion that can be achieved by a **static_cast** or a **reinterpret_cast**, combined with a **const_cast**.

Casts are best avoided. In most cases, consider their use a sign of poor programming. Exceptions to this rule are presented in §17.8 and §25.4.1. The C-style cast and function-style casts have the nasty property that you don't have to understand exactly what the cast is doing (§27.3.4). Prefer the named casts when you cannot avoid an explicit type conversion.