
# 48. Continue Your C++ Education

You must continually learn if you want to become better at what you do, and many resources are available to you to continue your C++ education.

## Know How To Ask Questions

Kate Gregory has published an [excellent article on how to ask questions](1). Some key points are:

- Don't use screenshots
- Use good variable names
- Add some tests
- Listen to what people are telling you

## Conferences And Local User Groups

There is almost certainly one near you. Check out the [ISO C++ Conferences Worldwide List](2) and [Meeting C++ User Groups List](3).

I am finishing this book during the global COVID-19 pandemic. So conferences and user groups are mostly held on right now. But this presents an attractive opportunity for many.

> ^1http://www.regcons.com/KateBlog/HowToAskForCodingHelp.aspx
2https://isocpp.org/wiki/faq/conferences-worldwide
3https://meetingcpp.com/usergroups/

Continue Your C++ Education

Many of those conferences and user groups are now meeting online. It’s now possible for us all to attend each other’s user groups. The North Denver Metro C++ Meetup⁴ for example, regularly has one attendee from Thailand each month.

> Note from the author: when interacting with the C++ community member to treat others with dignity and respect; be patient; take time to understand the rules and norms of the particular community which you are interacting.

## C++ Weekly

This book references C++ Weekly throughout as a resource to go back to more information and examples to share with your coworkers. At this moment, the show has been going for 235 weeks straight with many special editions, extras, and live streams.

## cpppreference.com

The website is fantastic, but you might not know that you can create an account and customize the content to the version of C++ you are using. Also, you can execute examples and download an offline version⁵!

## Hire a Trainer to Come Onsite for Your Company

Team training gets your team thinking in a new direction, improves morale, and boosts employee retention. Since you made it this far, I’m going to offer you a coupon.

⁴https://www.m.com/North-Denver-Metro-C-Meetup/
⁵https://en.cpppreference.com/w/Cppreference

## YouTube

- Andreas Fertig’s Channel^6
- C++ Weekly (Author’s Channel)^7
- CopperSpice^8

> ^6https://www.youtube.com/channel/UCxJflfPGHS3_nRDv1u-Qu8g
^7https://www.youtube.com/c/JasonTurner-lefticus
^8https://www.youtube.com/cospice

# 49. Thank You

## Sponsors

Thank you to all of my Book Supporter patrons who helped make this book possible!

- Adam Albright
- Adam P Shield
- Alejandro Lucena
- Alexander Roper
- Andrei Sebastian Cîmpean
- Anton Smyk
- Arman Imani
- Bill Baker
- Björn Fahller
- Brendan Nolan
- Clint Rajaniemi
- Corentin Gay
- David C Black
- Dennis Börm
- Emyr Williams
- Fedor Alekseev
- Florian Sommer
- Gwendolyn Hunt
- Ivan Pakhomov
- Jack Glass
- Jaewon Jung
- Jeff Bakst
- Kacper Kołodziej
- Lars Ove Larsen
- Magnus Westin

Thank You

Martin Hammerchmidt
Matt Godbolt
Matthew Guidry
Michael Pearce
Michael Pettit
Natalya Kochanova
Olafur Waage
Panos Gourgaris
Ralph Jeffrey Steinhagen
Reiner Eiteljoerge
Sebastian Raaphorst
Sergii Zaiets
Tim Butler
Tobias Dieterich
Tomasz Cwik
Yacob Cohen-Arazi

## Reviewers

Craig Scott and Alexander Roper, thank you for extensive notes and feedback during prerelease.

# 50. Bonus: Understand The Lambda

A surprising complexity hides behind the simple lambda of C++. Initially added in C++11, it was initially constrained. With each version of C++, the lambda becomes more flexible and powerful.

Lambdas reverse some of the defaults from the rest of C++. Default const and automatically constexpr when possible; they give us some of what we wish the rest of the language could have.

Lambda grammar:

```
lambda-expression:
lambda-introducer lambda-declarator(opt) compound-statement
lambda-introducer < template-parameter-list > requires-clause(opt)
lambda-declarator(opt) compound-statement
```

```
lambda-introducer:
  [ lambda-capture(opt) ]
lambda-declarator:
  ( parameter-declaration-clause ) decl-specifier-seq(opt)
  noexcept-specifier(opt) attribute-specifier-seq(opt)
  trailing-reverse-type(opt) requires-clause(opt)
```

If you can read standard-cpp, you can dig into all of the features of C++20's lambdas yourself.

## Bonus: Understand The Lambda

Allowed lambdas as of C++20.

```
// valid empty lambda, does nothing
[]{}

// optional to have parameter list
[](){}

// C++17 explicit constexpr and return void
[]() constexpr -> void {};
// immediately invoked lambda
auto i = [](){{ return 42; }();
// Not allowed before C++17, because constexpr
constexpr auto j = [](){{ return 42; }();
// generic lambda, C++14
[](auto x){ return x + 42; };
// variadic lambda, C++14
[](auto... x){ return std::vector<int>(x...) }; };
// capture by copy, C++11
[i](){ return i + 42; };
// generalized capture, C++14 (what's the type of i)
[i = 42]{ return i + 42; };
// stateful lambda, C++11
[i]() mutable { return ++i; };
// explicit template, C++20
<typename T>(T x){ return x + 42; };

// generic lambda returning a C++20 lambda with variadic
// capture by move.
[... = val]{ return (val + ...); };
```

If you understand every aspect of lambdas, you know about C++.

This is why I put together my class on YouTube.

> https://www.youtube.com/playlist?list=PLs3KjaCtOwAwiwm-frBs-

In 2018 when compilers started supporting C++20s new lambdas, I implemented this standards-compliant version of std::bind using lambdas.

(Continued on next page.)

# Bonus: Understand The Lambda

```
template <std::size_t Idx>
struct Placeholder {};
```

```
template <typename T>
struct Bound {
    constexpr decltype(auto) operator()(auto &&param) const {
        return t(std::forward<decltype(param)>(param)...);
    }
    T t;
};
```

```
template <typename T>
Bound(T) -> Bound<T>;
```

```
template <std::size_t Idx>
constexpr decltype(auto) get_param(const Placeholder<Idx>&,
 T&&) {
    return std::get<Idx>(t);
}
```

```
template <typename Param, typename T>
constexpr decltype(auto) get_param(Param &&param, T&&) {
    return std::forward<Param>(param);
}
```

```
template <typename Param, typename T>
constexpr decltype(auto) get_param(const Bound<Param>&b,
 T&&) {
    return std::apply(b, std::forward<T>(t));
}
```

```
constexpr decltype(auto) bind(auto &&callable, auto &&param) {
    return Bound{
[callable = std::forward<decltype(callable)>(callable),
... xs = std::forward<decltype(param)>(param)
(auto &&values) {
    auto passed_params =
        std::forward_as_tuple<decltype(values)>(values)...;
    return std::invoke(callable,
        get_param(xs, passed_params)...);
}
};
};
```

# Exercise: Understand the given example and critique it.

What should I have done differently with the above example? Can it be constrained with concepts? Does it need better names? What would you do differently?

³https://godbolt.org/z/hhde3P3
