
This was known as the Y2K bug or the millennium bug. It proved to be a bonanza for older contractors, who toured the computers of the world effecting repairs on 25-year-old systems at considerable expense. Disaster was largely averted because the problem was identified in sufficient time and there were enough engineers available to put things right.

However, if the engineers had planned for the future instead, had assumed that their code would run “forever,” and were writing the code at a point in time when four-digit integers occupied the same space as two-digit integers, this would have been avoided. It would have been clear that two digits was NOT enough to represent all dates that may be required, and at least a third digit would be needed, and really a fourth digit would just be simpler all around to accommodate the turn of the millennium.

Incidentally, this is not the only date problem. Linux has a similar problem with measuring time in seconds since January 1, 1970. This was stored as a 32-bit signed integer, which means it will roll over on January 19, 2038. I say “was”: from Linux 5.6 the problem was solved.

An important pair of career skills is therefore writing code for the future and learning to read code from the past.

## Staying on top of developments to the standard

C++ is developing all the time. With every publication of a new standard there comes a cornucopia of new language features and library additions. There is no especial virtue in simply using the most novel features; they should be used where they give definite and concrete benefit. However, the C++ community is very fortunate to have many excellent teachers ready to unfold and reveal all these new things to us. Finding these resources is made easier in four ways.

### IsoCpp

First of all, there is isocpp.org. This is the home of C++ on the Web and is run by the Standard C++ Foundation. This is a Washington 501(c)(6) not-for-profit organization whose purpose is to support the C++ software developer community and promote the understanding and use of modern Standard C++ on all compilers and platforms. On this site you can find a

## Chapter 1.2

### F.51: Where there is a choice, prefer default arguments over overloading

#### Introduction

API design is a valuable skill. As you decompose a problem into its constituent abstractions, you need to identify the abstractions and design an interface for them, giving the client clear and unambiguous usage instructions in the form of a completely obvious set of carefully named functions. There is a saying that code should be self-documenting. While this is a lofty ambition, it is in API design that you should try hardest to meet this goal.

Codebases grow. They just do. There is no getting away from it. Time passes, more abstractions are discovered and encoded, more problems are solved, and the problem domain itself expands to accommodate more use cases. This is fine and perfectly normal. It is part of the usual operation of development and engineering.

As these extra abstractions are added to the codebase, the problem of unambiguously naming things rears its ugly head. Naming is hard. That phrase will come up a lot in your programming career. Sometimes you want to let the client, which is often yourself, do the same thing but in a slightly different way.

This is where overloading may seem like a good idea. The difference between two abstractions may simply be the arguments that are passed to them; in all other respects they are semantically identical. Function overloading allows you to reuse a function name with a different set of parameters. But if they are indeed semantically identical, can you express that difference in terms of a default argument? If so, your API will be simpler to understand.

## 2025年6月 KS2 第1章课后测

姓名：____ 班级：____ 学号：____

### 一、选择题（每题2分，共10分）

1. 下列最能体现我国社会主义民主政治的本质属性的是（ ）
   - A. 全过程人民民主
   - B. 选举民主
   - C. 协商民主
   - D. 基层民主

2. 下列属于我国基本政治制度的是（ ）
   - A. 人民代表大会制度
   - B. 中国共产党领导的多党合作和政治协商制度
   - C. 社会主义市场经济体制
   - D. 民族区域自治制度

3. 以下公民参与民主生活的做法中，不正确的是（ ）
   - A. 参加公交价格调整听证会
   - B. 在选举中投出自己神圣的一票
   - C. 在网络平台上随意发表言论
   - D. 通过人大代表反映小区停车难问题

### 二、简答题（5分）

1. 为什么说全过程人民民主是最广泛、最真实、最管用的民主？（5分）

![](img/1f717ab54347ad0154ca00897b584f1a_37_0.png)

```cpp
office make_office(float floor_space, int staff, bool two_floors = false);
```

One speedy recompilation later and all remains right with the world. Unfortunately, the demons of domain expansion are not finished with you yet: it turns out that the single-floor offices sometimes need the name of the building they will be situated in. You, the ever-accommodating engineer, expand your function's parameter list once again:

```cpp
office make_office(float floor_space, int staff, bool two_floors = false,
                   std::string const& building_name = {});
```

You reimplement your function, but it irritates you. There are four arguments, the final argument will only be needed if the third argument is false, and it all looks messy and complicated. You decide to overload your function:

```cpp
office make_office(float floor_space, int staff, bool two_floors = false);
office make_office(float floor_space, int staff,
                   std::string const& building_name);
```

You now have what is known as a function overload set, and it is up to the compiler to choose which member of the set to invoke according to the arguments passed in. The client is forced to call the correct function when a building must be identified. Identification implies a single-floor office.

For example, some client code may wish to create an office with 24,000 square meters of space for 200 people. The office is situated on one floor in a building called “Eagle Heights.” The correct invocation is therefore

integral promotion, while an object of type `float` can be promoted to an object of type `double`, known as floating-point promotion.

Conversions differ from promotions in that they may change the value, which may cost precision. For example, a floating-point value can be converted to an integer, rounding to the nearest integer value. Also, integral and floating-point values, unscoped enumerations, pointers, and pointer-to-member types can be converted to `bool`. These three ranks are C concepts and are unavoidable if compatibility with C is to be maintained.

That partially covers standard conversion sequences. User-defined conversions take place in two ways: either through a non-explicit constructor, or through a non-explicit conversion operator. This is what we are expecting to happen in our example: we are expecting our `char const*` to convert to a `std::string` via the non-explicit constructor which takes a `char const*`. This is as plain as the nose on your face. Why have we dragged you through this exposition on overloading?

### Back to the example

In the above example, the client is expecting the `char const*` to participate in a user-defined conversion to a `std::string`, and for that temporary value argument to be passed as a reference to `const` to the second function’s third parameter.

However, user-defined conversion sequences take second priority to standard conversion sequences. In the earlier paragraph on conversions, we identified a standard conversion from pointer to `bool`. If you have ever seen older code that passes raw pointers around the codebase, you will have seen something like

```cpp
if (ptr) {
    ptr->do_thing();
}
```

The condition of the `if` statement is a pointer, not a `bool`, but a pointer can be converted to false if it is zero. This is a brief and idiomatic way of writing
