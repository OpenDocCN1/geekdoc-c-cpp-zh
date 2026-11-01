

- 避免, 31–40
- 封装和数据隐私, 34–37
- 元组，返回, 186–188
- 两阶段初始化，目的, 23–24
- 类型别名，声明, 42
- 类型双关, 250
- 类型安全
  - 缓冲区大小, 255–257
  - 强制转换, 250–253
  - 目的, 247–248
  - union 关键字, 249–250
  - unsigned 关键字, 253–255
- 类型
  - 内置, 82–83
  - 用于枚举, 197–198
  - 用于货币, 71
  - 作为可变, 263
  - 分类, 239–240
  - 变化, 7–8

## U
- 枚举的底层类型, 197–198
- union 关键字, 249–250
- unique_ptr, 122–124, 297–298
- 无作用域枚举
  - 隐式转换, 198–200
  - 优先使用有作用域枚举而非无作用域, 193–200
- unsigned 关键字, 253–255
- 用户定义的转换序列, 17
- using 声明, 42, 171–172
- using 指令, 43
  - 在全局作用域，避免, 169–178
  - 在嵌套命名空间中, 172–174
  - 重载的命名空间函数与, 175–176
  - 目的, 172
- using enum 声明, 43
- using 关键字, 171–172, 307–308

## V
变量

C 风格声明, 276–277

先声明后初始化, 277–278

延迟声明, 275–283

最大程度延迟声明, 278–280

variant 对象, 249

变化封装

C++ 的扩展, 6

基本类型, 7–8

头文件, 7

语言级别和编译器, 5–6

监管约束, 8

运行时环境, 4–5

向量, 233

抽象中的动词/名词, 39–40

virtual 关键字, 44–45

## W
可写数据，最小化显式共享, 97–105

## Y
千年虫问题, 9–10

## Z
Z80 汇编语言, 49–50, 285–286

零初始化, 222–223

## C/C++ 编程
图书、电子书和视频

![](img/1f717ab54347ad0154ca00897b584f1a_430_0.png)

无论您是编程新手、刚开始学习 C 或 C++ 的程序员，还是多年来一直使用 C 或 C++ 编程，InformIT 都为您提供所需的 C/C++ 图书、电子书和视频课程。

- 来自语言创建者的官方指南
- 入门读物和教程
- 参考书
- 关于编码和设计的实用指南

访问 informit.com/cplusplus 阅读样章、购物并观看精选产品的视频课程。

![](img/1f717ab54347ad0154ca00897b584f1a_432_0.png)

## 在 informit.com/register 注册您的产品

获取额外福利，并在下次购买时节省 35%

- 自动收到一张下次购买 35% 优惠券，有效期为 30 天。请查看您的 InformIT 购物车或账户页面上的“管理代码”部分找到您的代码。
- 下载可用的产品更新。
- 访问可用的附加资料。*
- 勾选复选框以接收我们的消息，并获得新版本和相关产品的独家优惠。

*注册福利因产品而异。福利将列在您账户页面的“已注册产品”下。

## InformIT.com——值得信赖的技术学习来源

InformIT 是 Pearson 旗下信息技术品牌的在线家园，Pearson 是全球领先的教育公司。在 InformIT.com，您可以：

- 购买我们的图书、电子书、软件和视频培训
- 利用我们的特别优惠和促销活动 (informit.com/promotions)
- 注册接收特别优惠和内容通讯 (informit.com/newsletters)
- 访问数千个免费章节和视频课程

与 InformIT 联系——访问 informit.com/community

## 代码片段

许多图书包含编程代码或配置示例。为了优化这些元素的显示，请在单列、横向模式下查看电子书，并将字体大小调整为最小设置。除了以可重排文本格式呈现代码和配置外，我们还包含了模仿纸质书呈现效果的代码图像；因此，当可重排格式可能影响代码清单的显示时，您会看到“单击此处查看代码图像”链接。单击该链接可查看与印刷版一致的代码图像。要返回上一页，请单击设备或应用上的“后退”按钮。

```
#if defined WIN32
auto a_pressed = bool{GetKeyState('A') & 0x8000 != 0};
#elif defined LINUX
auto a_pressed = /*really quite a lot of code*/
#endif
```

```
typedef __int i32; // older way of doing this: do not use now
```

```
office make_office(float floor_space, int staff);
```

```
office make_office(float floor_space, int staff, bool two_floors = false);
```

```
office make_office(float floor_space, int staff,bool two_floors = false,
    std::string const& building_name = {});
```

```
office make_office(float floor_space, int staff, bool two_floors = false);
office make_office(float floor_space, int staff,
    std::string const& building_name);
```

```
auto eh_office = make_office(24000.f, 200, "Eagle Heights");
```

```
auto eh_office = make_office(24000.f, 200, "Eagle Heights"s);
```

```
enum class floors {one, two};
office make_office(float floor_space, int staff,
    floors floor_count = floors::one);
office make_office(float floor_space, int staff,
    std::string const& building_name);
```

```
office make_office(float floor_space,int staff,bool two_floors = false,
    std::string const& building_name = {});
```

```
office make_office(float floor_space, int staff,bool two_floors,
std::string const& building_name = {});
```

```
office make_office(float floor_space, int staff,bool two_floors = false,
    std::string const& building_name);
```

```
office make_office(float floor_space, int staff, floors floor_count);
office make_office(float floor_space, int staff,
    std::string const& building_name);
```

```
office make_office_by_floor_count(float floor_space, int staff,
    floors floor_count);
office make_office_by_building_name(float floor_space, int staff,
    std::string const& building_name);
```

```
new_string = string1 + string2;
```

```
new_string = concatenate(string1, string2);
```

```
class piano
{
public:
    piano();

private:
    int number_of_keys;
    bool mechanical;
    std::string manufacturer;
};
```

```
piano::piano()
{
    number_of_keys = 88;
    mechanical = true;
    manufacturer = "Yamaha";
}
```

```
piano::piano()
  : number_of_keys(88)
  , mechanical(true)
  , manufacturer("Yamaha")
{}
```

```
class piano
{
public:
    // piano(); // no longer needed

private:
    int number_of_keys = 88;
    bool mechanical = true;
    std::string manufacturer = "Yamaha";
};
```

```
class piano
{
public:
    piano()
        : number_of_keys(88)
        , mechanical(true)
        , manufacturer("Yamaha")
    {}
    piano(int number_of_keys_, bool mechanical_,
          std::string manufacturer_ = "Yamaha")
        : number_of_keys(number_of_keys_)
        , mechanical(mechanical_)
        , manufacturer(std::move(manufacturer_))
    {}
    piano(int number_of_keys_) {
        number_of_keys = number_of_keys_;
        mechanical = false;
        manufacturer = "";
    }

private:
    int number_of_keys;
    bool mechanical;
    std::string manufacturer;
};
```

```
class piano
{
public:
    piano() = default;
    piano(int number_of_keys_, bool mechanical_, std::string manufacturer_)
    : number_of_keys(number_of_keys_)
    , mechanical(mechanical_)
    , manufacturer(manufacturer_)
    {}
    piano(int number_of_keys_) {
        number_of_keys = number_of_keys_;
    }

private:
    int number_of_keys = 88;
    bool mechanical = true;
    std::string manufacturer = "Yamaha";
};
```

```
class x_wrapper
{
public:
    explicit x_wrapper(int x_) : x(x_) {}
    int get_x() const { return x; } // this is a getter
    void set_x(int x_) { x = x_; } // this is a setter

private:
    int x;
};
```

