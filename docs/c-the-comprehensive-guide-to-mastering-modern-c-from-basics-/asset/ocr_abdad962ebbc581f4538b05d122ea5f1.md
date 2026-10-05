# # 5.6 Names

Each identifier can be written in a specific style with the following properties:

+   - Capital or lowercase character at the beginning
- Capital letters throughout
- Underline _ or CamelCase for word boundaries
- Start or end with an underscore _

It makes sense to differentiate among different groups by these visual aspects and always maintain this. The same applies here: get used to a style and discuss it with your colleagues.

One possibility is as follows:

+   - *Variables* start with a lowercase character and continue in CamelCase, as inValue, btnCancelNow.
- *Class variables* use this style as well, but end with underscore, for example, data_, fwrite.
- *Functions and methods* are formatted like variables, as in getData(), assertEquals()==or instead of CamelCase, they can use underscores, as in get_data(), assert_equal()(this is sometimes called snake_case).
- *Simple types* are set in lowercase with underscore, but with a suffix, as in money_type.
- *Classes* start with an uppercase character in CamelCase, as in Data, VideoImage.