
在清单 14.7 中，你可以看到 `testImplMultimap.cpp` 测试模块的源代码，该模块反过来测试 `impl_multimap.cpp` 库模块。

```cpp
// https://godbolt.org/z/r9sdhaazz (uses boost library)
/* private header from lib directory: */
#include "impl_multimap.hpp"                 // to test
// we define init_unit_test_suite() ourselves, so DO NOT set:
/* #define BOOST_TEST_MODULE grammar */
#include <boost/test/included/unit_test.hpp>
#include <memory>                             // shared ptr
#include <vector>
#include <string>
using namespace boost::unit_test;
using namespace std::literals::string_literals;
using std::string; using std::vector;
/* === A test class for the class under test === */
using UnderTest = qw::impl_multimap::index_impl;
class ImplMultimapTest {                         // class with test methods
public:
    void testConstants() {
        BOOST_REQUIRE_EQUAL(UnderTest::prefix().length(), UnderTest::q()-1);
        BOOST_REQUIRE_EQUAL(UnderTest::suffix().length(), UnderTest::q()-1);
        for(size_t i = 0; i < UnderTest::q()-1; ++i) {
            BOOST_CHECK_EQUAL(UnderTest::prefix()[i], '^');
            BOOST_CHECK_EQUAL(UnderTest::suffix()[i], '$');
        }

        BOOST_TEST(UnderTest::q() == 3u);
        BOOST_TEST(UnderTest::prefix() == "^^"s);
        BOOST_TEST(UnderTest::suffix() == "$$"s);
    }

    /** === qgramify === */
    void testQgramifyEmpty() {
        UnderTest inst{};
        auto result = inst._qgramify(""s);
        vector<string> expected{"^^"s, "^$"s};
        BOOST_CHECK_EQUAL_COLLECTIONS
            result.begin(), result.end(), expected.begin(), expected.end());
    }

    void testQgramify1() {
        UnderTest inst{};
        auto result = inst._qgramify("a"s);
        vector<string> expected{"^^"s, "^a$"s, "a$$"s};
        BOOST_CHECK_EQUAL_COLLECTIONS
            result.begin(), result.end(), expected.begin(), expected.end());
    }

    void testQgramify2() {
        UnderTest inst{};
        auto result = inst._qgramify("ab");
        vector<string> expected{"^^a", "^^ab", "ab$", "b$$"};
        BOOST_CHECK_EQUAL_COLLECTIONS(
            result.begin(), result.end(), expected.begin(), expected.end());
    }

    void testQgramify3() {
        UnderTest inst{};
        auto result = inst._qgramify("abc");
        vector<string> expected{"^^a", "^^ab", "abc", "ab$", "bc$", "c$$"};
        BOOST_CHECK_EQUAL_COLLECTIONS(
            result.begin(), result.end(), expected.begin(), expected.end());
    }

    void testAdd_nodups() {
        UnderTest inst{};                    /* arrange */
        BOOST_REQUIRE_EQUAL(inst.size(), 0u); /* assert */
        inst.add("", "");                    /* act */
        BOOST_CHECK_EQUAL(inst.size(), 1u);   /* assert */
        inst.add("ENTRY", "entry");          /* act */
        BOOST_CHECK_EQUAL(inst.size(), 2u);   /* assert */
        inst.add("OTHER", "other");          /* act */
        BOOST_CHECK_EQUAL(inst.size(), 3u);   /* assert */
    }

    void test_getBestMatch_empty() {
        UnderTest inst{};
        auto result = inst.getBestMatch("any");
        BOOST_CHECK_EQUAL(result, "");
    }

    void test_getBestMatch_one() {
        /* arrange */
        UnderTest inst{};
        inst.add("HOLDERTEUFEL", "holderteufel");
        /* act */
        auto result = inst.getBestMatch("ROBERT");
        BOOST_CHECK_EQUAL(result, "holderteufel");
    }

    void test_getBestMatch_exact() {
        /* arrange */
        UnderTest inst{};
        inst.add("BERLIN", "Berlin");
        inst.add("HAMBURG", "Hamburg");
        inst.add("DORTMUND", "Dortmund");
        inst.add("STUTTGART", "Stuttgart");
        inst.add("WYK", "Wyk");
        /* act and assert */
        BOOST_CHECK_EQUAL(inst.getBestMatch("BERLIN"), "Berlin");
        BOOST_CHECK_EQUAL(inst.getBestMatch("HAMBURG"), "Hamburg");
        BOOST_CHECK_EQUAL(inst.getBestMatch("DORTMUND"), "Dortmund");
        BOOST_CHECK_EQUAL(inst.getBestMatch("STUTTGART"), "Stuttgart");
        BOOST_CHECK_EQUAL(inst.getBestMatch("WYK"), "Wyk");
    }

    void test_getBestMatch_close() {
        /* arrange */
        UnderTest inst{};
        inst.add("BERLIN", "Berlin");
        inst.add("HAMBURG", "Hamburg");
        inst.add("DORTMUND", "Dortmund");
        inst.add("STUTTGART", "Stuttgart");
        inst.add("WYK", "Wyk");
        /* act and assert */
        BOOST_CHECK_EQUAL(inst.getBestMatch("BERLIN"), "Berlin");
        BOOST_CHECK_EQUAL(inst.getBestMatch("BURC"), "Hamburg");
        BOOST_CHECK_EQUAL(inst.getBestMatch("DORTDORT"), "Dortmund");
        BOOST_CHECK_EQUAL(inst.getBestMatch("STUTTGART"), "Stuttgart");
        BOOST_CHECK_EQUAL(inst.getBestMatch("WIK"), "Wyk");
    }
    /* For new test methods: Don't forget to add to init_unit_test_suite() */
};

/* === Suite === */
test_suite* init_unit_test_suite( int argc, char* argv[] ) {
    auto tester = std::make_shared<ImplMultimapTest>();
    auto &ts = framework::master_test_suite();
    ts.add( BOOST_TEST_CASE( [&](){ tester->testConstants(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->testQgramifyEmpty(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->testQgramify1(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->testQgramify2(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->testQgramify3(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->testAdd_nodups(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->test_getBestMatch_empty(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->test_getBestMatch_one(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->test_getBestMatch_exact(); } ) );
    ts.add( BOOST_TEST_CASE( [&](){ tester->test_getBestMatch_close(); } ) );
    return nullptr;
}
```

**清单 14.7** 测试套件在此手动组装。

你也可以从外部文件加载数据。Boost.Test 还可以为你自动生成动态数据集。如果你对此感兴趣，请阅读 Boost.Test 文档中的“数据驱动测试用例”部分。

> **别忘了将其添加到测试套件中！**
>
> 实际上，我更喜欢显式方法，而不是使用 `BOOST_AUTO_TEST_CASE` 宏的自动魔法式方法。
>
> 然而，后者有一个巨大的优势：当你在源代码的某个位置编写新测试时，你不会忘记在代码的另一个位置也添加它。你简直不会相信这种情况在我身上发生过多少次：我添加了一个新测试，它最初应该失败，运行测试套件，然后纳闷：“为什么它通过了？”很简单，因为我忘了将新的测试方法添加到测试套件中。
>
> 对于 C++26，有一个关于*反射*的提案（P2996）。如果实现，框架将有可能自动从测试类中收集所有方法作为测试用例。在那之前，请记住：在手帕上打个结！

## 第15章

## 继承

### 本章提要

- **“Has-a”（有）关系**  
  无论是*聚合*还是*组合*，一个对象是另一个对象的一部分或与之相关。汽车*有*挡风玻璃，并且*有*车位。
- **“Is-a”（是）关系**  
  *继承*；一个特殊化对象也是一个更一般的对象。厢式货车*是*汽车。
- **组合**  
  一种“有”关系，其中对象由其他对象组成。
- **聚合**  
  一种“有”关系，其中对象与另一个对象相关。
- **重写**  
  在派生类中以相同签名重新定义基类的方法。
- **虚方法**  
  一种在运行时决定调用哪个重写变体的方法。
- **切片**  
  当你将派生类型转换为基类型并在该过程中丢失信息时；通常是错误类型的意外副本导致的结果——例如，在按值调用中。
- **运行时多态**  
  声明一个基类；在运行时使用派生类，但保留其派生属性。

继承是*面向对象编程*（OOP）的基本组成部分。伴随而来的是某些技术和词汇，我将在本章中介绍两者。

借助*继承*，你可以实现两件事：

- 你提高了*可复用性*并减少了*代码重复*；这些是更技术性的方面。
- 你实现了一种*设计*，从而在大型项目中创造清晰性；这是一个概念性的方面。
