
```cpp
class Base :
public Mixins... { public:
// the virtuality of foo() depends on its declaration
// (if any) in the base classes Mixins...
void foo() {
std::cout << "Base::foo()" << '\n';
}
};

template<typename... Mixins>
class Derived : public Base<Mixins...> {
public:
void foo() {
std::cout << "Derived::foo()" << '\n';
}
};

int main()
{
Base<NotVirtual>* p1 = new Derived<NotVirtual>;
p1->foo(); // calls Base::foo()

Base<Virtual>* p2 = new Derived<Virtual>;
p2->foo(); // calls Derived::foo()
}
```

This technique can provide a tool to design a class template that is usable both to instantiate concrete classes and to extend using inheritance. However, it is rarely sufficient just to sprinkle virtuality on some member functions to obtain a class that makes a good base class for more specialized functionality. This sort of development method requires more fundamental design decisions. It is therefore usually more practical to design two different tools (class or class template hierarchies) than to try to integrate them all into one template hierarchy.

## 21.4 Named Template Arguments

Various template techniques sometimes cause a class template to end up with many different template type parameters. However, many of these parameters often have reasonable default values. A natural way to define such a class template may look as follows:

```cpp
template<typename Policy1 = DefaultPolicy1,
typename Policy2 = DefaultPolicy2,
typename Policy3 = DefaultPolicy3,
typename Policy4 = DefaultPolicy4>
class BreadSlicer {
```

```cpp
public Discriminator<Setter2,2>,
public Discriminator<Setter3,3>,
public Discriminator<Setter4,4> {
};
```

Note the use of an intermediate Discriminator template. It is needed to allow the various Setter types to be identical. (You cannot have multiple direct base classes of the same type. Indirect base classes, on the other hand, can have types that are identical to those of other bases.) As announced earlier, we’re collecting the defaults in a base class:

```cpp
// name default policies as P1, P2, P3, P4
class DefaultPolicies {
public:
using P1 = DefaultPolicy1;
using P2 = DefaultPolicy2;
using P3 = DefaultPolicy3;
using P4 = DefaultPolicy4;
};
```

However, we must be careful to avoid ambiguities if we end up inheriting multiple times from this base class. Therefore, we ensure that the base class is inherited virtually:

```cpp
// class to define a use of the default policy values
// avoids ambiguities if we derive from DefaultPolicies more than once
class DefaultPolicyArgs : virtual public DefaultPolicies {
};
```

Finally, we also need some templates to override the default policy values:

```cpp
template<typename Policy>
class Policy1_is : virtual public DefaultPolicies {
public:
using P1 = Policy; // overriding type alias
};
```

```cpp
template<typename Policy>
class Policy2_is : virtual public DefaultPolicies {
public:
using P2 = Policy; // overriding type alias
};
```

```cpp
template<typename Policy>
class Policy3_is : virtual public DefaultPolicies {
public:
using P3 = Policy; // overriding type alias
};
```

```cpp
template<typename Policy>
class Policy4_is : virtual public DefaultPolicies {
public:
using P4 = Policy; // overriding type alias
};
```

With all this in place, our desired objective is achieved. Now let’s look at what we have by example. Let’s instantiate a BreadSlicer<> as follows:

```cpp
BreadSlicer<Policy3_is<CustomPolicy>> bc;
```

For this BreadSlicer<> the type Policies is defined as

```cpp
PolicySelector<Policy3_is<CustomPolicy>,
DefaultPolicyArgs,
DefaultPolicyArgs,
DefaultPolicyArgs>
```

With the help of the Discriminator<> class templates, this results in a hierarchy in which all template arguments are base classes (see Figure 21.4). The important point is that these base classes

Figure 21.4. Resulting type hierarchy of BreadSlicer<>::Policies

all have the same virtual base class DefaultPolicies, which defines the default types for P1, P2, P3, and P4. However, P3 is redefined in one of the derived classes—namely, in Policy3_is<>. According to the domination rule, this definition hides the definition of the base class. Thus, this is not an ambiguity.⁶

Inside the template BreadSlicer you can refer to the four policies by using qualified names such as Policies::P3. For example:

```cpp
template<...>
class BreadSlicer {
...
public:
void print () {
Policies::P3::doPrint();
}
...;
};
```

In inherit/namedtmp1.cpp you can find the entire example.

We developed the technique for four template type parameters, but it obviously scales to any reasonable number of such parameters. Note that we never actually instantiate objects of the helper class that contain virtual bases. Hence, the fact that they are virtual bases is not a performance or memory consumption issue.

## 21.5 Afternotes

Bill Gibbons was the main sponsor behind the introduction of the EBCO into the C++ programming language. Nathan Myers made it popular and proposed a template similar to our BaseMemberPair to take better advantage of it. The Boost library contains a considerably more sophisticated template, called compressed_pair, that resolves some of the problems we reported for the MyClass template in this chapter. boost::compressed_pair can also be used instead of our BaseMemberPair.

CRTP has been in use since at least 1991. However, James Coplien was first to describe them formally as a class of patterns (see [CoplienCRTP]). Since then, many applications of CRTP have been published. The phrase parameterized inheritance is sometimes wrongly equated with CRTP. As we have shown, CRTP does not require the derivation to be parameterized at all, and many forms of parameterized inheritance do not conform to CRTP. CRTP is also sometimes confused with the Barton-Nackman trick (see Section 21.2.1 on page 497) because Barton and Nackman frequently used CRTP in combination with friend name injection (and the latter is an important component of the Barton-Nackman trick). Our use of CRTP with the Barton-Nackman trick to provide operator implementations follows the same basic approach as the Boost.Operators library ([BoostOperators]), which provides an extensive set of operator definitions. Similarly, our treatment of iterator facades follows that of the Boost.Iterator library ([BoostIterator]) which provides a rich, standard-library compliant iterator interface for a derived type that provides a few core iterator operations (equality, dereference, movement), and also addresses tricky issues involving proxy iterators (which we did not address for the sake of brevity). Our ObjectCounter example is almost identical to a technique developed by Scott Meyers in [MeyersCounting].

The notion of mixins has been around in Object-Oriented programming since at least 1986 ([Moon-Flavors]) as a way to introduce small pieces of functionality into an OO class. The use of templates for mixins in C++ became popular shortly after the first C++ standard was published, with two papers ([SmaragdakisBatoryMixins] and [EiseneckerBlinnCzarnecki]) describing the approaches commonly used today for mixins. Since then, it’s become a popular technique in C++ library design.

Named template arguments are used to simplify certain class templates in the Boost library. Boost uses metaprogramming to create a type with properties similar to our PolicySelector (but without using virtual inheritance). The simpler alternative presented here was developed by one of us (Vandevoorde).

1 It may be worthwhile to read Section 16.2 on page 326 to understand how function template overloading works in modern C++.
2 Note that S is also a class associated with w because it is a template argument for the type of w. The specific rules for ADL are discussed in Section 13.2.1 on page 219.
3 To simplify the presentation, we ignore the presence of proxy iterators, whose dereference operation does not return a true reference. A complete implementation of an iterator facade, such as the one in [BoostIterator], would adjust the result types of operator -> and operator [] to account for proxies.
4 Again, we assume that the underlying iterator returns a reference, rather than a proxy, to simplify the presentation.
5 Note that a similar language extension for function call arguments was proposed (and rejected) earlier in the C++ standardization process (see Section 17.4 on page 358 for details).
6 You can find the domination rule in Section 10.2/6 in the first C++ standard (see [C++98]) and a discussion about it in Section 10.1.1 of [EllisStroustrupARM].
