

# C++17 - 完整指南

# 第一版

Nicolai M. Josuttis

本版本发布于 **2022-01-11.**

© 2022 by Nicolai Josuttis. All rights reserved.

未经作者事先许可，本出版物受版权保护，不得以任何形式或任何手段进行复制、存储于检索系统或传输，包括电子、机械、影印、录制或其他方式。

本书由 Nicolai M. Josuttis 使用 LaTeX 文档处理系统排版。

本书在 http://leanpub.com/cpp17 上发售。

这是一本 Leanpub 书籍。Leanpub 赋予作者和出版商 Lean Publishing 流程的力量。Lean Publishing 是指使用轻量级工具并通过多次迭代发布进行中的电子书，以获取读者反馈、调整直至获得合适的书籍，并在获得合适书籍后建立影响力。

# 目录

+   **前言**                                                                 xv
+     Versions of This Book . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xv
+     Acknowledgments . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xvii
+   
+   **关于本书**                                                              xix
+     What You Should Know Before Reading This Book . . . . . . . . . . . . . . . . . . . xix
+     Overall Structure of the Book . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xx
+     How to Read This Book . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xx
+     Error Terminology . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xx
+     The C++17 Standard . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xxi
+     Example Code and Additional Information . . . . . . . . . . . . . . . . . . . . . . xxi
+     Feedback . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . xxi
+   
+   **第一部分：基础语言特性**                                              1
+   
+   **1 结构化绑定**                                                       3
+     1.1  Structured Bindings in Detail . . . . . . . . . . . . . . . . . . . . . . . . . 4
+     1.2  Where Structured Bindings Can Be Used . . . . . . . . . . . . . . . . . . . . 7
+       1.2.1  Structures and Classes . . . . . . . . . . . . . . . . . . . . . . . . . . 8
+       1.2.2  Raw Arrays . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
+       1.2.3  std::pair, std::tuple, and std::array . . . . . . . . . . . . . . . . . 9
+     1.3  Providing a Tuple-Like API for Structured Bindings . . . . . . . . . . . . 11
+     1.4  Afternotes . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 19
+   
+   **2 if 和 switch 的初始化**                                         21
+     2.1  if with Initialization . . . . . . . . . . . . . . . . . . . . . . . . . . . . 21
+   2.2 switch with Initialization ................................................... 23
+   2.3 Afternotes ............................................................... 24
+   
+   3 Inline Variables .............................................................. 25
+   3.1 Motivation for Inline Variables .............................................. 25
+   3.2 Using Inline Variables ...................................................... 27
+   3.3 constexpr Now Implies inline For Static Members ................................ 28
+   3.4 Inline Variables and thread_local ............................................ 29
+   3.5 Afternotes ............................................................... 31
+   
+   4 Aggregate Extensions ........................................................... 33
+   4.1 Motivation for Extended Aggregate Initialization .............................. 34
+   4.2 Using Extended Aggregate Initialization ...................................... 34
+   4.3 Definition of Aggregates ..................................................... 36
+   4.4 Backward Incompatibilities ................................................... 36
+   4.5 Afternotes ............................................................... 37
+   
+   5 Mandatory Copy Elision or Passing Unmaterialized Objects ....................... 39
+   5.1 Motivation for Mandatory Copy Elision for Temporaries ....................... 39
+   5.2 Benefit of Mandatory Copy Elision for Temporaries ............................ 41
+   5.3 Clarified Value Categories ................................................... 42
+   5.3.1 Value Categories ....................................................... 42
+   5.3.2 Value Categories Since C++17 ............................................ 44
+   5.4 Unmaterialized Return Value Passing .......................................... 45
+   5.5 Afternotes ............................................................... 46
+   
+   6 Lambda Extensions .............................................................. 47
+   6.1 constexpr Lambdas ........................................................... 47
+   6.1.1 Using constexpr Lambdas .................................................. 49
+   6.2 Passing Copies of this to Lambdas ............................................ 50
+   6.3 Capturing by const Reference ................................................ 53
+   6.4 Afternotes ............................................................... 53
+   
+   7 New Attributes and Attribute Features .......................................... 55
+   7.1 Attribute [[nodiscard]] ..................................................... 55
+   - 7.2 Attribute [[maybe_unused]] ................ 57
+   - 7.3 Attribute [[fallthrough]] ................ 58
+   - 7.4 General Attribute Extensions ................ 58
+   - 7.5 Afternotes ................ 59

# 8 其他语言特性

+   - 8.1 Nested Namespaces ................ 61
+   - 8.2 Defined Expression Evaluation Order ................ 62
+   - 8.3 Relaxed Enum Initialization from Integral Values ................ 65
+   - 8.4 Fixed Direct List Initialization with auto ................ 66
+   - 8.5 Hexadecimal Floating-Point Literals ................ 67
+   - 8.6 UTF-8 Character Literals ................ 68
+   - 8.7 Exception Specifications as Part of the Type ................ 69
+   - 8.8 Single-Argument static_assert ................ 72
+   - 8.9 Preprocessor Condition __has_include ................ 73
+   - 8.10 Afternotes ................ 73

# 第二部分：模板特性

# 9 类模板参数推导

+   - 9.1 Use of Class Template Argument Deduction ................ 77
+   - 9.1.1 Copying by Default ................ 79
+   - 9.1.2 Deducing the Type of Lambdas ................ 80
+   - 9.1.3 No Partial Class Template Argument Deduction ................ 81
+   - 9.1.4 Class Template Argument Deduction Instead of Convenience Functions ................ 83
+   - 9.2 Deduction Guides ................ 84
+   - 9.2.1 Using Deduction Guides to Force Decay ................ 85
+   - 9.2.2 Non-Template Deduction Guides ................ 86
+   - 9.2.3 Deduction Guides versus Constructors ................ 86
+   - 9.2.4 Explicit Deduction Guides ................ 87
+   - 9.2.5 Deduction Guides for Aggregates ................ 88
+   - 9.2.6 Standard Deduction Guides ................ 89
+   - 9.3 Afternotes ................ 93

# 第三部分：新库组件 133

# 15 std::optional<> 135

+   15.1 Using std::optional<> ................................... 135

+   15.1.1 Optional Return Values ................................... 135

+   15.1.2 Optional Arguments and Data Members ....................... 137

+   15.2 std::optional<> Types and Operations ........................ 139

+   15.2.1 std::optional<> Types ................................... 139

+   15.2.2 std::optional<> Operations ............................... 139

+   15.3 Special Cases ............................................. 146

+   15.3.1 Optional of Boolean or Raw Pointer Values ................. 146

+   15.3.2 Optional of Optional .................................... 146

+   15.4 Afternotes ............................................... 147

# 16 std::variant<> 149

+   16.1 Motivation for std::variant<> .............................. 149

+   16.2 Using std::variant<> ...................................... 150

+   16.3 std::variant<> Types and Operations ........................ 152

+   16.3.1 std::variant<> Types .................................... 152

+   16.3.2 std::variant<> Operations ............................... 153

+   16.3.3 Visitors ............................................... 157

+   16.3.4 Valueless by Exception .................................. 161

+   16.4 Polymorphism and Heterogeneous Collections with std::variant . 162

+   16.4.1 Geometric Objects with std::variant ...................... 163

+   16.4.2 Other Heterogeneous Collections with std::variant ........ 165

+   16.4.3 Comparing variant Polymorphism ........................... 167

+   16.5 Special Cases with std::variant<> .......................... 168

+   16.5.1 Having Both bool and std::string Alternatives ............ 168

+   16.6 Afternotes ............................................... 168

# 17 std::any 171

+   17.1 Using std::any ............................................ 171

+   17.2 std::any Types and Operations .............................. 174

+   17.2.1 Any Types .............................................. 174

+   17.2.2 Any Operations ......................................... 174

