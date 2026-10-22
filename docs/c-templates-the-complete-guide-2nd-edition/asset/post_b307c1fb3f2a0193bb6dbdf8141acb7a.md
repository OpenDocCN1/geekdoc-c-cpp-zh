
template parameter pack 188, 200
    with deduced type 298, 569
template template argument 85, 197
template template parameter 83, 187, 398
    argument matching 85, 197
    versus member template 398
temploid 181
temporaries 630
temporary perfect forwarding 167
temporary materialization 676
terminology 151, 759
this-> 70, 238
*this
    value category 686
tokenization 224
    maximum munch 226
to_string() for bitsets 79
Touton, James 321
tracer 657
trailing return type 282
traits 385, 638, 769, see type traits as predicates 410
    detecting noexcept 443
    factory 422
    fixed 386
    for incomplete types 734
    for value and reference 638
    iterator_traits 399
    parameterized 394
    policy traits 458
    standard library 697
    template 769
    value traits 389
    variadic templates, multiple type traits 734
    versus policy class 397
translation unit 154, 663, 769

+   transparency 324  
+   trivial type 712  
+   true constant 769  
+   TrueType 411  
+   true_type 413, 699  
+   　implementation 411  
+   tuple 575, 769  
+   　EBCO 593  
+   　get() 598  
+   　operator[] 599  
+   tuple_element 308  
+   tuple_size 308  
+   two-phase lookup 6, 238, 249, 769  
+   two-phase translation 6  
+   two-stage lookup 249  
+   type alias 38  
+   　arguments 194  
+   　category see type category closure type 310  
+   　complete 154, 245  
+   　composite type (category) 702  
+   　conversion 74  
+   　definition xxxii, 38, see type alias dependent 223, 228  
+   　dependent name 228  
+   　erasure 523  
+   　for bool_constant 699  
+   　for integral_constant 698  
+   　function 401  
+   　incomplete 154  
+   　metaprogramming 531  
+   　of *this 686  
+   　of container element 401  
+   　parameter 185  
+   　POD 151  
+   　POD trait 713  
+   　predicates 410

+   primary type (category) 702
+   qualification 448, 460
+   read-only parameter 458
+   requirement 743
+   safety 376
+   standard-layout 712
+   trivial 712
+   utilities in standard library 697
+   type alias 769
+   type category composite 702
+     primary 702
+   typedef 38
+   type-dependent expression 217, 233
+   typeid 138
+   type_info 138
+   typelist 455, 549
+   typename 4, 67, 185, 229
+     future 354
+     type parameter 4
+   TypeT<> 460
+   type template 769
+   type traits 164, see traits as predicates 410
+     factory 422
+     for incomplete types 734
+     standard library 697
+     _t version 40, 83
+     unexpected behavior 164
+     variadic templates, multiple type traits 734
+   __type_traits 462
+   
+   U
+   UCN 216
+   unary fold 208
+   unbounded polymorphism 376
+   underlying_type 716
+   unevaluated operand 133, 667

+   union anonymous 246  
+     definition 668  
+     discriminated 603  
+     qualification 456  
+     template 180  
+   unit types metaprogramming 534  
+   universal character name 216  
+   universal reference 93, 111, 769, see forwarding reference unknown  
+     specialization 223, 228  
+       member of 229, 240  
+   unnamed namespace 666  
+   unqualified-id 216  
+   unqualified lookup 216  
+   unqualified name 216  
+   unrolling loops 533  
+   Unruh, Erwin 352, 545  
+   UnruhPrimeOrig 757  
+   user-defined conversion 195, 769  
+   using 4, 231  
+   using declaration 239  
+     dependent name 231  
+     variadic expressions 65  
+   utilities in the standard library 697

# V

+   valarray 648  
+   Vali, Faisal 321  
+   value as parameter 45  
+     for bool_constant 699  
+     for integral_constant 698  
+     functions 401  
+   value category 282, 673, 770  
+     *this 686  
+     before C++11 673  
+     decltype 678  
+     of string literals 674

+   of template parameters 187
+   since C++11 674
+   value-dependent expression 234
+   value initialization 68
+   value metaprogramming 529
+   value traits 389
+   value_type
+     for bool_constant 699
+     for integral_constant 698
+   Vandevoorde, David 242, 321, 516, 547, 647
+   VandevoordeJosuttisTemplates1st 757
+   VandevoordeSolutions 758
+   varargs interface 55
+   variable template 80, 447, 770
+   constexpr 473
+   variadic base classes 65
+     using 65
+   variadic template 55, 190, 200
+     and enable_if 735
+     deduction guide 64
+     fold expression 58
+     multiple type traits 734
+     overload resolution 335
+     perfect forwarding 281
+   variant 603
+   vector 23
+   vector 380
+   Veldhuizen, Todd 546, 647
+   VeldhuizenMeta95 758
+   virtual
+     function dispatch table 257
+     instantiation 246
+     member templates 182
+     parameterized 510
+   visitor for Variant 617

void
  and decltype(auto) 162
  as template parameter 6
  in templates 361
void*
  conversion to 689
  template parameter 186
void_t 420, 437
Voutilainen, Ville 267

W
whitespace 770
Willcock, Jeremiah 488
Witt, Thomas 515
wrap function calls 162

X
xvalue 674, 770

Z
zero initialization 68

```
int* const bookmark;    // the pointer cannot change, but the value pointed to can
```

```
using CHARS = char*;
using CPTR = CHARS const; // constant pointer to chars
```

```
typedef char* const CPTR;  // constant pointer to chars
```

```
using CPTR = char* const;  // constant pointer to chars
```

```
typedef char* CHARS;
typedef const CHARS CPTR;  // constant pointer to chars
```

```
typedef const char* CPTR;  // pointer to constant chars
```

basics/max1.hpp

```
template<typename T>
T max (T a, T b)
{
    // if b < a then yield a else yield b
    return  b < a ? a : b;
}
```

```
template< comma-separated-list-of-parameters >
```

```
template<class T>
T max (T a, T b)
{
    return  b < a ? a : b;
}
```

# 关于开展2024年社会治安综合治理宣传月活动的通知

各部门、直属各单位：

为扎实推进社会治安综合治理工作，全面提升广大干部职工的法律意识和安全意识，营造和谐稳定的企业文化氛围，经研究决定，于2024年8月在系统内开展社会治安综合治理宣传月活动。现将有关事项通知如下：

一、总体要求

深入贯彻落实党的二十大精神，坚持以人民为中心的发展思想，通过开展形式多样的宣传教育活动，进一步提高干部职工参与社会治安综合治理的积极性，为集团高质量发展营造平安稳定的发展环境。

二、活动时间

2024年8月1日至8月31日。

三、宣传重点

+   1. 突出平安建设宣传
+   2. 突出法治宣传教育
+   3. 突出反诈骗、反邪教宣传
+   4. 突出安全生产宣传

四、工作要求

（一）加强组织领导。各单位要高度重视，成立专项工作小组，制定具体实施方案，确保宣传月活动有序开展。

（二）创新活动形式。充分利用宣传栏、电子屏、微信公众号等多种载体，拓宽宣传渠道，提升宣传实效。

（三）注重总结提升。活动开展期间，请各单位及时报送宣传动态及图文资料，并于9月10日前报送活动总结。

特此通知。

xxx公司

2024年7月20日

```
double f1 = 3.4;
double f2 = -6.7;
std::cout << "max(f1,f2): " << ::max(f1,f2) << '\n';

std::string s1 = "mathematics";
std::string s2 = "math";
std::cout << "max(s1,s2): " << ::max(s1,s2) << '\n';
}
```

max(7,i):  42
max(f1,f2): 3.4
max(s1,s2): mathematics

```
double max (double, double);
std::string max (std::string, std::string);
```

```
template<typename T>
T foo(T*)
{
}

void* vp = nullptr;
foo(vp);            // OK: deduces void foo(void*)
```

```
```cpp
std::complex<float> c1, c2;    // doesn’t provide operator <
...
::max(c1,c2);                  // ERROR at compile time
```
```

```
template<typename T>
void foo(T t)
{
    undeclared();      // first-phase compile-time error if undeclared() unknown
    undeclared(t);      // second-phase compile-time error if undeclared(T) unknown
    static_assert(sizeof(int) > 10,      // always fails if sizeof(int)<=10
        "int too small");
    static_assert(sizeof(T) > 10,      // fails if instantiated for T with size <=10
        "T too small");
}
```

```
template<typename T>
T max (T const& a, T const& b)
{
    return  b < a ? a : b;
}
```

```
```cpp
template<typename T>
T max (T a, T b);
...
int const c = 42;
max(i, c);        // OK: T is deduced as int
max(c, c);        // OK: T is deduced as int
int& ir = i;
max(i, ir);       // OK: T is deduced as int
int arr[4];
foo(&i, arr);     // OK: T is deduced as int*
```
```

```
max(4, 7.2);      // ERROR: T can be deduced as int or double
std::string s;
foo("hello", s);  // ERROR: T can be deduced as char const[6] or std::string
```
