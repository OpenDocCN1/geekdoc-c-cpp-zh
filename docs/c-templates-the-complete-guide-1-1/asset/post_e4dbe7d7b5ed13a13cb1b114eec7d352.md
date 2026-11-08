
```cpp
y[i] {
}
```

This formulation requires some more work for each class that will be mixed in, so classes such as label and color will need to become class templates. However, the mixed-in class can now tailor their behavior to the specific instance of the derived class they've been mixed into. For example, we can mix the previously discussed Object counter template into the root: the number of objects created by each class can be counted by that mixin with other application-specific mixins as well.

### 21.3.2 Parameterized Virtuality

Mixins also allow us to indirectly parameterize other attributes of the derived class, such as the virtuality of a member function. A simple example shows this rather surprising technique:

inherit/virtual.cpp

```cpp
#include <iostream>

class NotVirtual {
};

class Virtual {
public:
    virtual void foo() {
    }
};

template<typename... Mixins>
class Base :
    public Mixins... {
public:
    // the virtuality of foo() depends on its declaration
    // (if any) in the base classes Mixins.
    void foo() {
        std::cout << "Base::foo()\n";
    }
};

template<typename... Mixins>
class Derived : public Base<Mixins...> {
public:
    void foo() {
        std::cout << "Derived::foo()\n";
    }
};

int main()
{
    Base<NotVirtual> *p1 = new Derived<NotVirtual>();
    p1->foo(); // calls Base::foo()

    Base<Virtual> *p2 = new Derived<Virtual>();
    p2->foo(); // calls Derived::foo()
}
```

This technique can provide a tool to design a class template that is usable both to instantiate concrete classes and to extend using inheritance. However, it is rarely sufficient just to specialize virtuality on some member functions to obtain a class that makes a good base class for more specialized functionality. This sort of development method requires more fundamental design decisions. It is therefore usually more practical to design two different tools (a class or class template hierarchy) than try to fit everything into one template hierarchy with many different template type parameters. However, many of these parameters often have reasonable default values. A natural way to define such a class template may look as follows:

```cpp
template<typename Policy1 = DefaultPolicy1,
         typename Policy2 = DefaultPolicy2,
         typename Policy3 = DefaultPolicy3,
         typename Policy4 = DefaultPolicy4>
class ThreadLocker
{
};
```

Presumably, such a template can often be used with the default template argument values using the syntax `ThreadLocker<>`. However, if a non-default argument must be specified, all preceding arguments must be specified too (even though they may have the default value).

Clearly, it would be unattractive to be able to use a construct akin to `ThreadLocker<Policy3 = Custom>` rather than `ThreadLocker<DefaultPolicy1, DefaultPolicy2, Custom>`, as is the case right now. In what follows we develop a technique to enable almost exactly that.

```cpp
template<typename PolicySet1 = DefaultPolicySet1,
         typename PolicySet2 = DefaultPolicySet2,
         typename PolicySet3 = DefaultPolicySet3,
         typename PolicySet4 = DefaultPolicySet4>
class PolicySelector
{
    PolicySet1 policySet1;
    PolicySet2 policySet2;
    PolicySet3 policySet3;
    PolicySet4 policySet4;
};
```

Our technique consists of placing the default type values in a base class and overriding some of them through derivation. Instead of directly specifying the type arguments, we provide them through member functions. For example, we could write `Great<Policy1>`, because each template argument can describe one of the policies, the defaults can be different. In other words, at a higher level, every template parameter is equivalent:

```cpp
template<typename Policy1, typename Policy2,
         typename Policy3, typename Policy4>
class PolicySelector : public PolicySelectorBase<Policy1,
                                                 Policy2,
                                                 Policy3,
                                                 Policy4>
{
public:
    PolicySelector() {}
};
```

The remaining challenge is to write the policy selector template. It has to merge the different template arguments into a single type that overrides default policy types along with members with whichever non-default type is specified. This merging can be achieved using inheritance:

```cpp
// PolicySelector<A,B,C,D> creates A,B,C,D as base
// classes
// Discriminator to allow having more than one base class
template<typename Base>
class Discriminator : public Base
{
};

template<typename Select1, typename Select2,
         typename Select3, typename Select4>
class PolicySelector : public Discriminator<Select1>,
                       public Discriminator<Select2>,
                       public Discriminator<Select3>,
                       public Discriminator<Select4>
{
};
```

Note the use of an intermediate `Discriminator` template. It is needed to allow the various `Selector` types to be identical. You cannot have multiple direct base classes of the same type. Indirect base classes, on the other hand, can have types that are identical to those of other bases.

As a proposed policy, we're collecting the defaults in a base class.

```cpp
// Name default policies as P1, P2, P3, P4
class DefaultPolicies
{
public:
    using P1 = DefaultPolicy1;
    using P2 = DefaultPolicy2;
    using P3 = DefaultPolicy3;
    using P4 = DefaultPolicy4;
};
```

However, we must be careful to avoid ambiguities if we end up inheriting multiple times from this base class. Therefore, we ensure that the base class is inherited virtually:

```cpp
template<typename Policy>
class Policy1 : virtual public DefaultPolicies {
public:
    using P1 = Policy; // overriding type alias
};

template<typename Policy>
class Policy2 : virtual public DefaultPolicies {
public:
    using P2 = Policy; // overriding type alias
};

template<typename Policy>
class Policy3 : virtual public DefaultPolicies {
public:
    using P3 = Policy; // overriding type alias
};

template<typename Policy>
class Policy4 : virtual public DefaultPolicies {
public:
    using P4 = Policy; // overriding type alias
};
```

With all this in place, our desired objective is achieved. Now let's look at what we have by example. Let's instantiate a BreadSlices class:

```cpp
BreadSlices<Policy3, IceCreamPolicy> bc;
```

For this class, the output is defined as

```cpp
PolicySelector<Policy3, IceCreamPolicy>,
    DefaultPolicy<...>,
    DefaultPolicy<...>,
    DefaultPolicy<...>
```

With the help of the Discriminator<> class templates, this results in a hierarchy in which all the subtypes are derived from the base classes (see Figure 21-4). The important point is that these base classes all have the same virtual base class DefaultPolicies, which defines the default types for P1, P2, P3, and P4. However, P3 is redefined in one of the derived classes—namely, in Policy3—and according to the dominance rule, this definition hides the definition of the base class. Thus, this is not an ambiguity.

*Figure 21-4. Resolving type hierarchy of BreadSlices<Policies>*

Inside the template BreadSlices you can refer to the four policies by using qualified names such as `Policies::P3`. For example

```cpp
template<...>
class BreadSlices {

public:
    void print() {
        Policies::P1::doPrint();
    }
};
```

In inherit/named1.cpp you can find the entire example.

We developed the technique for four template parameters, but it obviously scales to any reasonable number of such parameters. Note that we never actually instantiate objects of the helper class that contain virtual bases. In fact, the fact that they are virtual bases is not a performance or memory consumption issue.

## 21.5 Afternotes

Bill Gibbons was the main sponsor behind the introduction of the EBCO into the C++ programming language. Nathan Myers made it popular and proposed a template similar to our BaseMemberPair to take better advantage of it. The Boost library contains a considerably more sophisticated template, called compressed_pair, that addresses some of the problems of the C++ template in this chapter.

The simple approach to the EBCO in this chapter is based on the idea that the implementation of a base class can be optimized away, if it has no data members and no virtual functions. However, the C++ standard does not require this optimization, and there are implementations that do not perform it.

C++ and many forms of parameterized inheritance do not conform to EBCO. EBCO is especially useful in the Boost library, where it is used to implement function objects and other generic programming techniques.

The notion of mixins has been around in Object-Oriented programming since at least 1986 (MoonFlavors) as a way to introduce small pieces of behavior into a class hierarchy.
