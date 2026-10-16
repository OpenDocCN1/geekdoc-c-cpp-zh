
```
class moneypunct_byname : public moneypunct<C, Intl> {
// …
};
```

The **decimal_point()**, **thousands_sep()**, and **grouping()** members behave as in **numpunct**.

The **curr_symbol()**, **positive_sign()**, and **negative_sign()** members return the string to be used to represent the currency symbol (for example, **$**, **¥**, **INR**, **DKK**), the plus sign, and the minus sign, respectively. If the **International** template argument is **true**, the **intl** member will also be **true**, and “international” representations of the currency symbols will be used. Such an “international” representation is a four-character C-style string. For example:

+   “USD”
+   “DKK”
+   “EUR”

The last (invisible) character is a terminating zero. The three-letter currency identifier is defined by the ISO-4217 standard. When **International** is **false**, a “local” currency symbol, such as **$**, **£**, and **¥**, can be used.

A **pattern** returned by **pos_format()** or **neg_format()** is four **parts** defining the sequence in which the numeric value, the currency symbol, the sign symbol, and whitespace occur. Most common formats are trivially represented using this simple notion of a pattern. For example:

+   +$ 123.45 // {sign, symbol, space, value} where positive_sign() returns “+”
+   $+123.45 // {symbol, sign, value, none} where positive_sign() returns “+”
+   $123.45 // {symbol, sign, value, none} where positive_sign() returns “”
+   $123.45- // {symbol, value, sign, none}
+   −123.45 DKK // {sign, value, space, symbol}
+   ($123.45) // {sign, symbol, value, none} where negative_sign() returns “()”
+   (123.45DKK) // {sign, value, symbol, none} where negative_sign() returns “()”

## Section 39.4.3.1 Money Punctuation

Representing a negative number using parentheses is achieved by having **negative_sign()** return a string containing the two characters **()**. The first character of a sign string is placed where **sign** is found in the pattern, and the rest of the sign string is placed after all other parts of the pattern. The most common use of this facility is to represent the financial community’s convention of using parentheses for negative amounts, but other uses are possible. For example:

+   −$123.45 // {sign, symbol, value, none} where negative_sign() returns “−”
+   // {sign, symbol, value, none} where negative_sign() returns “”

Each of the values **sign**, **value**, and **symbol** must appear exactly once in a pattern. The remaining value can be either **space** or **none**. Where **space** appears, at least one and possibly more whitespace characters may appear in the representation. Where **none** appears, except at the end of a pattern, zero or more whitespace characters may appear in the representation.

Note that these strict rules ban some apparently reasonable patterns:

```
pattern pat = { sign, value , none , none }; // error : no symbol
```

The frac_digits() function indicates where the decimal_point() is placed. Often, monetary amounts are represented in the smallest currency unit (§39.4.3). This unit is typically one-hundredth of the major unit (for example, a ¢ is one-hundredth of a $), so frac_digits() is often 2.

Here is a simple format defined as a facet:

```
class My_money_io : public moneypunct<char,true> {
public:
explicit My_money_io(size_t r = 0) :moneypunct<char,true>(r) {}

char_type do_decimal_point() const { return '.'; } char_type do_thousands_sep() const { return ','; } string do_grouping() const { return "\003\003\003"; }

string_type do_curr_symbol() const { return "USD "; } string_type do_positive_sign() const { return ""; } string_type do_negative_sign() const { return "()"; }

int do_frac_digits() const { return 2; } // twodigits after decimal point

pattern do_pos_format() const { return pat; } pattern do_neg_format() const { return pat; } private:
static const pattern pat;
};
const pattern My_money_io::pat { sign, symbol, value , none };
```

## 39.4.3.2 Money Output

The money_put facet writes monetary amounts according to the format specified by moneypunct. Specifically, money_put provides put() functions that place a suitably formatted character representation into the stream buffer of a stream:

```
money_put<C,Out = ostreambuf_iterator<C>> facet (§iso.22.4.6.2) Put value v into buffer position b
```

```
Out put(Out b, bool intl, ios_base& s, C fill, long double v) const;
```

```
Out put(Out b, bool intl, ios_base& s, C fill, const string_type& v) const;
```

The intl argument indicates whether a standard four-character “international” currency symbol or a “local” symbol is used (§39.4.3.1).

Given money_put, we can define an output operator for Money (§39.4.3):

```
ostream& operator<<(ostream& s, Money m)
{
ostream::sentry guard(s); // see §38.4.1 if (!guard) return s;

try { const money_put<char>& f = use_facet<money_put<char>>(s.getloc()); if (m==static_cast<long long>(m)) { // m can be represented as a long long
if (f.put(s,true ,s,s. fill(),m).failed())
s.setstate(ios_base::badbit);
}
```

```
else {
ostringstream v;
v<<m; // convert to string representation
if (f.put(s,true ,s,s.fill(),v.str()).failed())
s.setstate(ios_base::badbit);
}
}
catch (...) {
handle_ioexception(s); // see §39.4.2.2
}
return s;
}
```

If a long long doesn’t have sufficient precision to represent the monetary value exactly, I convert the value to its string representation and output that using the put() that takes a string.

## 39.4.3.3 Money Input

The money_get facet reads monetary amounts according to the format specified by moneypunct. Specifically, money_get provides get() functions that extract a suitably formatted character representation from the stream buffer of a stream:

money_get<C,In = istreambuf_iterator<C>> facet (§iso.22.4.6.1) Read [b:e) into v, using formatting rules from s, reporting errors by setting r In get(In b, In e, bool intl, ios_base& s, ios_base::iostate& r, long double& v) const; In get(In b, In e, bool intl, ios_base& s, ios_base::iostate& r, string_type& v) const; A well-defined pair of money_get and money_put facets will provide output in a form that can be read back in without errors or loss of information. For example:

```
int main() {
Money m;
while (cin>>m)
cout << m << "\n";
}
```

The output of this simple program should be acceptable as its input. Furthermore, the output produced by a second run given the output from a first run should be identical to its input. A plausible input operator for Money would be:

```
istream& operator>>(istream& s, Money& m)
{
istream::sentry guard(s); // see _io.sentry_ if (guard) try {
ios_base::iostate state = 0; // good istreambuf_iterator<char> eos;
string str;
use_facet<money_get<char>>(s.getloc()).get(s,eos,true,state,str);
if (state==0 || state==ios_base::eofbit) { // set value only if get() succeeded long long i =
```

```
stoll(str); // §36.3.5
if (errno==ERANGE) {

state |= ios_base::failbit;
}
else {
m = i; // set value only if conversion to long long succeeded
}
s.setstate(state);
}
}
catch (...) {
handle_ioexception(s); // see §39.4.2.2
}
return s;
}
```

I use the **get()** that reads into a **string** because reading into a **double** and then converting to a **long long** could lead to loss of precision.

The largest value that can be exactly represented by a **long double** may be smaller than the largest value that can be represented by a **long long**.

## 39.4.4 Date and Time Formatting

Date and time formats are controlled by **time_get<C,In>** and **time_put<C,Out>**. The representation of dates and times used is **tm** (§43.6).

### 39.4.4.1 time_put

A **time_put** facet takes a point in time presented as a **tm** and produces a sequence of characters representing it using **strftime()** (§43.6) or an equivalent.

```
time_put<C,Out = ostreambuf_iterator<C>> facet (§iso.22.4.5.1)
Out put(Out s, ios_base& f, C fill, const tm* pt, const C* b, const C* e) const;
Out put(Out s, ios_base& f, C fill, const tm* pt, char format, char mod = 0) const;
Out do_put(Out s, ios_base& ib, const tm* pt, char format, char mod) const;
```

A call **s=put(s,ib,fill,pt,b,e)** copies **[b:e)** onto the output stream **s**. For each **strftime()** format character **x**, with optional modifier **mod**, it calls **do_put(s,ib,pt,x,mod)**. The possible modifier values are **0** (the default meaning “none”), **E**, or **O**. An overriding **p=do_put(s,ib,pt,x,mod)** is supposed to format the appropriate parts of **pt** into **s** and return a value pointing to the position in **s** after the last character written.

A **_byname** version (§39.4, §39.4.1) of **messages** is provided:

```
template<class C, class Out = ostreambuf_iterator<C>>
class time_put_byname : public time_put<C,Out>
{
// …
```
