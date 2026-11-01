
- avoiding, 31–40
- encapsulation and data privacy, 34–37
- tuples, returning, 186–188
- two-phase initialization, purpose of, 23–24
- type aliases, declaring, 42
- type punning, 250
- type safety
  - buffer size, 255–257
  - casting, 250–253
  - purpose of, 247–248
  - union keyword, 249–250
  - unsigned keyword, 253–255
- types
  - built-in, 82–83
  - for enumerations, 197–198
  - for money, 71
  - as mutable, 263
  - taxonomy of, 239–240
  - variations in, 7–8

## U
- underlying type for enumerations, 197–198
- union keyword, 249–250
- unique_ptr, 122–124, 297–298
- unscoped enumerations
  - implicit conversion, 198–200
  - preferring scoped over, 193–200
- unsigned keyword, 253–255
- user-defined conversion sequences, 17
- using declarations, 42, 171–172
- using directives, 43
  - at global scope, avoiding, 169–178
  - in nested namespaces, 172–174
  - overloaded namespace functions and, 175–176
  - purpose of, 172
- using enum declarations, 43
- using keyword, 171–172, 307–308

## V
variables

C-style declaration, 276–277

declare-then-initialize, 277–278

delaying declaration, 275–283

maximally delayed declaration, 278–280

variant object, 249

variation encapsulation

extensions to C++, 6

fundamental types, 7–8

header files, 7

language level and compiler, 5–6

regulatory constraints, 8

run-time environment, 4–5

vectors, 233

verbs/nouns in abstraction, 39–40

virtual keyword, 44–45

## W
writable data, minimizing explicit sharing, 97–105

## Y
Y2K bug, 9–10

## Z
Z80 assembly language, 49–50, 285–286

zero initialization, 222–223

## C/C++ Programming
Books, eBooks & Video

![](img/1f717ab54347ad0154ca00897b584f1a_430_0.png)

Whether you are new to programming, are a programmer just starting to learn C or C++, or have been programming with C or C++ for years, InformIT has the C/C++ books, eBooks, and video courses you need.

- Official guides from language creators
- Primers and tutorials
- References
- Pragmatic guides on coding and design

Visit informit.com/cplusplus to read sample chapters, shop, and watch video lessons from featured products.

![](img/1f717ab54347ad0154ca00897b584f1a_432_0.png)

## Register Your Product at informit.com/register

Access additional benefits and save 35% on your next purchase

- Automatically receive a coupon for 35% off your next purchase, valid for 30 days. Look for your code in your InformIT cart or the Manage Codes section of your account page.
- Download available product updates.
- Access bonus material if available.*
- Check the box to hear from us and receive exclusive offers on new editions and related products.

*Registration benefits vary by product. Benefits will be listed on your account page under Registered Products.

## InformIT.com—The Trusted Technology Learning Source

InformIT is the online home of information technology brands at Pearson, the world's foremost education company. At InformIT.com, you can:

- Shop our books, eBooks, software, and video training
- Take advantage of our special offers and promotions (informit.com/promotions)
- Sign up for special offers and content newsletter (informit.com/newsletters)
- Access thousands of free chapters and video lessons

Connect with InformIT—Visit informit.com/community

## Code Snippets

Many titles include programming code or configuration examples. To optimize the presentation of these elements, view the eBook in single-column, landscape mode and adjust the font size to the smallest setting. In addition to presenting code and configurations in the reflowable text format, we have included images of the code that mimic the presentation found in the print book; therefore, where the reflowable format may compromise the presentation of the code listing, you will see a “Click here to view code image” link. Click the link to view the print-fidelity code image. To return to the previous page viewed, click the Back button on your device or app.

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
