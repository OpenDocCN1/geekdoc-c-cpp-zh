
> ^1http://www.regcons.com/KateBlog/HowToAskForCodingHelp.aspx

2https://isocpp.org/wiki/faq/conferences-worldwide

3https://meetingcpp.com/usergroups/

继续你的 C++ 教育

许多此类会议和用户小组现在都在线上聚。现在我们所有人都可以参加彼此的用户小组。例如，北丹佛大罗区 C++ Meetup⁴ 每月定期有一个来自泰国的参与者。

> 作者注：在与 C++ 社区成员互动时要给予他人尊严和尊重；保持耐心；花时间理解你所身处的特定社区的规则和规范。

## C++ Weekly

本书全程引用 C++ Weekly 作为资源，以便回溯更多信息和与同事分享的示例。目前，该节目已连续播了 235 周，包含了许多特别节目、额外内容和直播。

## cpppreference.com

这个网站非常棒了，但你可能不知道你可以创建一个账户，并根据你正在使用的 C++ 版本自定义内容。此外，你还可以执行示例并下载离线版本⁵！

## 聘请培训师到公司现场培训

团队培训能让你的团队向新的方向思考，提高士气并增加员工留存。既然你已经看到这里了，我要给你一张优惠券。

⁴https://www.m.com/North-Denver-Metro-C-Meetup/

⁵https://en.cpppreference.com/w/Cppreference

## YouTube

- Andreas Fertig 的频道^6
- C++ Weekly (作者频道)^7
- CopperSpice^8

> ^6https://www.youtube.com/channel/UCxJflfPGHS3_nRDv1u-Qu8g
> ^7https://www.youtube.com/c/JasonTurner-lefticus
> ^8https://www.youtube.com/cospice

# 49. 感谢

## 赞助者

感谢所有帮助这本书成为可能的书籍支持者（Book Supporter）赞助！

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
感谢
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

## 审核员

Craig Scott 和 Alexander Roper，感谢他们在发布前提供的大量注释和反馈。

# 50. 奖励：理解 Lambda

C++ 简单的 lambda 背后隐藏着令人惊讶的复杂性。它最初在 C++11 中引入，当时受到限制。随着每个 C++ 版本的发布，lambda 变得更加灵活和强大。

Lambda 反转了 C++ 其他部分的某些默认设置。默认的 `const` 并在尽可能的情况下自动 `constexpr`；它们带我们了一些我们希望语言其他部分具备的功能。

Lambda 语法：

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

如果你能读懂标准-cpp，你就可以自己研究 C++20 lambda 的所有特性。

## 奖励：理解 Lambda

C++ 简单的 lambda 背后隐藏着令人惊讶的复杂性。它最初在 C++11 中引入，当时受到限制。随着每个 C++ 版本的发布，lambda 变得更加灵活和强大。

Lambda 反转了 C++ 其他部分的某些默认设置。默认的 `const` 并在尽可能的情况下自动 `constexpr`；它们带我们了一些我们希望语言其他部分具备的功能。

在 2018 年当编译器开始支持 C++20 新 lambda 时，我使用 lambda 实现了这个标准的 `std::bind` 版本。

（见下一页。）

# 奖励：理解 Lambda

```
template <std::size_t Idx>
struct Placeholder {};
```

20 18 年当编译器开始支持 C++20 新 lambda 时，我使用 lambda 实现了这个标准的 `std::bind` 版本。

```cpp
template <typename T>
struct Bound {
    constexpr decltype(auto) operator()(auto &&param) const {
        return t(std::forward<decltype(param)>(param)...;
    }
    T t;
};
```

```cpp
template <typename T>
Bound(T) -> Bound<T>;
```

```cpp
template <std::size_t Idx>
constexpr decltype(auto) get_param(const Placeholder<Idx>&,
 T&&) {
    return std::get<Idx>(t);
}
```

```cpp
template <typename Param, typename T>
constexpr decltype(auto) get_param(Param &&param, T&&) {
    return std::forward<Param>(param);
}
```

```cpp
template <typename Param, typename T>
constexpr decltype(auto) get_param(const Bound<Param>&b,
 T&&) {
    return std::apply(b, std::forward<T>(t));
}
```

```cpp
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

## 练习：理解给定示例并进行评判

对于上面的示例，我应该做哪些不同的改进？可以使用概念（concepts）进行约束吗？需要更好的命名吗？你会有什么不同的做法？

³https://godbolt.org/z/hhde3P3
