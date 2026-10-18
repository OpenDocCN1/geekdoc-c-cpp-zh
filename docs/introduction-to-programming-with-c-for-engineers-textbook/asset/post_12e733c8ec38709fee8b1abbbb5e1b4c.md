
Composition is a stronger form of aggregation association since it implies ownership of the Class_B object ("part") by the Class_A object ("whole"). This means a part can belong to at most one composite, and the part object lives as long as the whole composite.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_312_0.png)

A car should have a built-in engine. Hence, the TCar class (Class_A) owns an object of the TEngine class (Class_B). What is important here is that TCar and its TEngine objects are strictly lifetime-related. That is, if TCar is destroyed, so is its TEngine counterpart. In practice, the link from Class_A to object(s) of Class_B is performed by a reference or a pointer (here we use a smart pointer; see Section 5.3).

**Table 4.4 (continued)**

| Class relation | Description | UML diagram | Examples |
|---|---|---|---|
| **Inheritance (is-a)** | Allows specialization in the form of Class_B, which is derived from the base class Class_A. In this sense, Class_B “is-a” type of Class_A. Class_B inherits members of Class_A. It can also add its own members and change their behavior by defining its own virtual functions. It is possible for a class to be derived from more than one base class (*multiple inheritance*). The base class is called a *superclass*, *mother class*, or *parent class*. The derived class is frequently called a *subclass* or *child class*. | ![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_313_0.png)<br>UML diagram showing Class_A as the base class and Class_B as the derived class, connected by an inheritance arrow and labeled “is a” relation. | <code>class GasEngine : public TEngine<br>{<br>};<br>class DieselEngine : public TEngine<br>{<br>};<br>class ElectricEngine : public TEngine<br>{<br>};</code> |

During derivation, an access filter is provided for the base class, as shown in Figure 4.2. The access filter plus the member access types limit base members to the more restrictive access rule. That is, if a member is declared protected but the derivation is private, then the member becomes private in the derived class, and so on. If no access filter is provided, then private is assumed. In this case, all base members become private in the derived class. Inheritance of this type is in contrast to the _static_ polymorphism provided by the template mechanism (Section 4.13).

| Relation multiplicity | Description | Class member visibility | Description | Type of relation | Description |
|---|---|---|---|---|---|
| 0 | No instance | + | Public |  | Association |
| 0..1 | No instance or exactly one | - | Private |  | Dependency |
| 1 | Exactly one instance | # | Protected |  | Inheritance |
| 0..* | Zero or more instances | / | Derived (inheritance) |  | Aggregation |
| 1..* | One or more instances | ~ | Package (libraries) |  | Composition |

In recent decades, more complex relations between classes have been observed, which repeat from project to project regardless of differences in minor details. These are known as *design patterns* (Gamma et al. 1994). In the following sections, we will also present a few of the most practical ones.

## 4.10 Example Project – Extending Functionality Through Class Inheritance with `TComplexQuadEq`

In Section 3.15, we presented the `TQuadEq` class, which represents quadratic equations in the real domain. Depending on the values of its three parameters, there can be zero, one, or two solutions, or roots. However, two roots always exist in the realm of complex numbers, as we know from Section 4.4. How can we extend `TQuadEq` to return the `TComplex` roots? Do we need to write everything from the beginning, or can we somehow reuse parts of `TQuadEq`? We can use one of the basic principles of OOP: class inheritance, as shown in Figure 4.14.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_315_0.png)

**Figure 4.14** UML class diagram showing the inheritance relation between the classes `TQuadEq` and `TComplexQuadEq`. `TComplexQuadEq` inherits data members and the `ComputeDelta` function from the base class `TQuadEq`. There is also a relation between the `TComplexQuadEq` and `TComplex` classes – `TComplexQuadEq` knows and uses objects of `TComplex`.

As already presented in Table 4.4, inheritance allows a derived class to “possess” all the features of the base class. As a result, the derived class can concentrate on its specific behavior. Also, using the virtual mechanism discussed in the next section, it is possible to adjust the operation of some of the member functions defined in the base class.

Listing 4.22 shows the definition of the `TComplexQuadEq` class derived from `TQuadEq`. Inheritance relations are expressed in the class definition, on line [9]. It follows the scheme shown in Figure 4.15.

```cpp
using CppBook::TComplex;

class TComplexQuadEq : public TQuadEq
{
```

Implementation of the two member functions of the `TComplexQuadEq` class is shown in Listing 4.23. In the complex domain, if this is a proper quadratic equation, then there are always roots. This is expressed on line [11] of the `GetNumOfRoots`, whose definition begins on line [3].

```cpp
#include "ComplexQuadEq.h"

TComplexQuadEq::EEqType TComplexQuadEq::GetNumOfRoots( const double delta ) const
{
    if( Get_a() == 0.0 )
    {
        return Get_b() == 0.0 ? EEqType::kLinContra : EEqType::kLinNone;
    }
    else
    {
        // In this class the sign of delta is not important
        return delta == 0.0 ? EEqType::kOne : EEqType::kTwo;
    }
}
```

`GetRoots`, defined on line [14], also operates in the complex domain. On line [17], the `delta` parameter is computed with a call to the `ComputeDelta` member from the base class. This is possible since `ComputeDelta` was declared public in `TQuadEq`. This parameter is then passed on line [21] to `GetNumOfRoots` from the `TComplexQuadEq` class. Depending on the return type of the equation, the correct action is undertaken by the `switch` on line [23]. If there are two member functions with the same name, one in the base class and the other in the derived class, then the derived class hides the definition from the base class, rather than overloading it. But the base function, if accessible, can also be called from the derived class, as we will see soon.

The most interesting two cases, `EEqType::kOne` and `EEqType::kTwo`, are treated together—there is no break statement between them. First, the denominator is checked to be sure its value is large enough. If not, then an exception is thrown on line [59]. Then, the two cases related to the sign of the `delta` parameter are resolved on line [62]. In both cases, we need to initialize the two `TComplex` objects. For the complex domain, this is computed on lines [65–69]. However, if there are only real roots, the imaginary parts of both are set to 0.0, as accomplished on lines [75] and [78].

```cpp
TQuadEq::EEqType TComplexQuadEq::GetRoots( TComplex & root_1, TComplex & root_2 )
                                                    const
{
    auto delta( ComputeDelta() );       // Call a constructor for the built-in type

    const auto kDivThresh( 1e-36 );     // Used in assert to verify divisions

    EEqType equationTypeFlag = GetNumOfRoots( delta );

    switch( equationTypeFlag )
    {
        case EEqType::kNone:

            assert( false );             // should not happen
            break;
```
