
```cpp
long do_hash(const charT* low, const charT* high) const;
```

Returns: An integer value equal to the result of calling hash() on any other string for which do_compare() returns 0 (equal) when passed the two strings.

Recommended practice: The probability that the result equals that for another string which does not compare equal should be very small, approaching (1.0/numeric_limits<unsigned long>::max()).

## 28.4.5.2 Class template collate_byname [locale.collate.byname]

```cpp
namespace std {
  template<class charT>
  class collate_byname : public collate<charT> {
  public:
    using string_type = basic_string<charT>;

    explicit collate_byname(const char*, size_t refs = 0);
    explicit collate_byname(const string&, size_t refs = 0);

  protected:
    ~collate_byname();
  };
}
```

## 28.4.6 The time category [category.time]

### 28.4.6.1 General [category.time.general]

Templates time_get<charT, InputIterator> and time_put<charT, OutputIterator> provide date and time formatting and parsing. All specifications of member functions for time_put and time_get in the subclauses of 28.4.6 only apply to the specializations required in Tables 102 and 103 (28.3.1.2.1). Their members use their ios_base&, ios_base::iostate&, and fill arguments as described in 28.4, and the ctype<> facet, to determine formatting details.

### 28.4.6.2 Class template time_get [locale.time.get]

#### 28.4.6.2.1 General [locale.time.get.general]

```cpp
namespace std {
  class time_base {
  public:
    enum dateorder { no_order, dmy, mdy, ymd, ydm };
  };
```

```cpp
template<class charT, class InputIterator = istreambuf_iterator<charT>>
class time_get : public locale::facet, public time_base {
public:
  using char_type = charT;
  using iter_type = InputIterator;

  explicit time_get(size_t refs = 0);

  dateorder date_order() const { return do_date_order(); }
  iter_type get_time(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t) const;
  iter_type get_date(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t) const;
  iter_type get_weekday(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t) const;
  iter_type get_monthname(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t) const;
  iter_type get_year(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t) const;
  iter_type get(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t, char format, char modifier = 0) const;
  iter_type get(iter_type s, iter_type end, ios_base& f, ios_base::iostate& err, tm* t, const char_type* fmt, const char_type* fmtend) const;
}
```

Table 113: do_get_date effects [tab:locale.time.get.dogetdate]

| date_order() | Format |
|---|---|
| no_order | "%m/%d/%y" |
| dmy | "%d/%m/%y" |
| mdy | "%m/%d/%y" |
| ymd | "%y/%m/%d" |
| ydm | "%y/%d/%m" |

```cpp
iter_type do_get_weekday(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm* t) const;
iter_type do_get_monthname(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm* t) const;
```

7 Effects: Reads characters starting at s until it has extracted the (perhaps abbreviated) name of a weekday or month. If it finds an abbreviation that is followed by characters that can match a full name, it continues reading until it matches the full name or fails. It sets the appropriate struct tm member accordingly.

8 Returns: An iterator pointing immediately beyond the last character recognized as part of a valid name.

```cpp
iter_type do_get_year(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm* t) const;
```

9 Effects: Reads characters starting at s until it has extracted an unambiguous year identifier. It is implementation-defined whether two-digit year numbers are accepted, and (if so) what century they are assumed to lie in. Sets the t->tm_year member accordingly.

10 Returns: An iterator pointing immediately beyond the last character recognized as part of a valid year identifier.

```cpp
iter_type do_get(iter_type s, iter_type end, ios_base& f,
    ios_base::iostate& err, tm* t, char format, char modifier) const;
```

11 Preconditions: t points to an object.

12 Effects: The function starts by evaluating err = ios_base::goodbit. It then reads characters starting at s until it encounters an error, or until it has extracted and assigned those struct tm members, and any remaining format characters, corresponding to a conversion directive appropriate for the ISO/IEC 9945 function strptime, formed by concatenating '%', the modifier character, when non-NUL, and the format character. When the concatenation fails to yield a complete valid directive the function leaves the object pointed to by t unchanged and evaluates err |= ios_base::failbit. When s == end evaluates to true after reading a character the function evaluates err |= ios_base::eofbit.

13 For complex conversion directives such as %C, %x, or %X, or directives that involve the optional modifiers E or O, when the function is unable to unambiguously determine some or all struct tm members from the input sequence [s, end), it evaluates err |= ios_base::eofbit. In such cases the values of those struct tm members are unspecified and may be outside their valid range.

14 Remarks: It is unspecified whether multiple calls to do_get() with the address of the same struct tm object will update the current contents of the object or simply overwrite its members. Portable programs should zero out the object before invoking the function.

15 Returns: An iterator pointing immediately beyond the last character recognized as possibly part of a valid input sequence for the given format and modifier.

### 28.4.6.3 Class template time_get_byname [locale.time.get.byname]

```cpp
namespace std {
  template<class charT, class InputIterator = istreambuf_iterator<charT>>
  class time_get_byname : public time_get<charT, InputIterator> {
  public:
    using dateorder = time_base::dateorder;
    using iter_type = InputIterator;
}
```

## 第二章 财务管理环境和组织

### 第一节 财务管理环境

#### 一、财务管理环境的概念

财务管理环境是指对企业财务活动产生影响的企业内部和外部各种因素的总称。企业的财务管理活动是在一定的环境条件下进行的，财务管理环境的好坏直接影响企业财务管理活动的顺利开展。

#### 二、财务管理环境的分类

- 1. 按涉及的范围分为宏观财务管理环境和微观财务管理环境
- 2. 按与企业的关系分为内部财务管理环境和外部财务管理环境
- 3. 按环境的变化状况分为静态环境和动态环境

#### 三、财务管理环境的内容

- 1. 经济环境
- 2. 金融环境
- 3. 法律环境
- 4. 市场环境
- 5. 管理体制环境
- 6. 企业内部环境

宏观经济环境包括经济体制、经济周期、经济发展水平、宏观经济政策等因素；微观经济环境包括企业的组织形式、产品结构、管理水平、企业文化等。

金融环境主要是指金融市场环境，包括金融市场、金融机构、金融工具等。法律环境是指企业财务管理活动中所应遵循的各种法律、法规和规章。

企业内部环境包括企业组织形式、企业治理结构、企业管理制度、企业文化等。企业各项财务活动都受上述环境因素的影响和制约。

```cpp
template<class charT>
    class messages : public locale::facet, public messages_base {
    public:
        using char_type  = charT;
        using string_type = basic_string<charT>;

        explicit messages(size_t refs = 0);

        catalog open(const string& fn, const locale&) const;
        string_type get(catalog c, int set, int msgid,
            const string_type& dfault) const;
        void close(catalog c) const;

        static locale::id id;

    protected:
        ~messages();
        virtual catalog do_open(const string&, const locale&) const;
        virtual string_type do_get(catalog, int set, int msgid,
            const string_type& dfault) const;
        virtual void do_close(catalog) const;
    };
}
```

1 Values of type messages_base::catalog usable as arguments to members get and close can be obtained only by calling member open.

### 28.4.8.2.2 Members [locale.messages.members]

catalog open(const string& name, const locale& loc) const;

1 Returns: do_open(name, loc).

string_type get(catalog cat, int set, int msgid, const string_type& dfault) const;

2 Returns: do_get(cat, set, msgid, dfault).

void close(catalog cat) const;

3 Effects: Calls do_close(cat).

### 28.4.8.2.3 Virtual functions [locale.messages.virtuals]

catalog do_open(const string& name, const locale& loc) const;

1 Returns: A value that may be passed to get() to retrieve a message from the message catalog identified by the string name according to an implementation-defined mapping. The result can be used until it is passed to close().

2 Returns a value less than 0 if no such catalog can be opened.

3 Remarks: The locale argument loc is used for character set code conversion when retrieving messages, if needed.

string_type do_get(catalog cat, int set, int msgid, const string_type& dfault) const;

4 Preconditions: cat is a catalog obtained from open() and not yet closed.

5 Returns: A message identified by arguments set, msgid, and dfault, according to an implementation-defined mapping. If no such message can be found, returns dfault.

void do_close(catalog cat) const;

6 Preconditions: cat is a catalog obtained from open() and not yet closed.

7 Effects: Releases unspecified resources associated with cat.

8 Remarks: The limit on such resources, if any, is implementation-defined.
