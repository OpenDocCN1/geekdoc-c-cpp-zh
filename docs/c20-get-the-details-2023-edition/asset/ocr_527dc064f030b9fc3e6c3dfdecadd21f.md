# Range adaptors in C++20

| View | Description |
|---|---|
| `std::views::all_t`<br>`std::views::all` | Converts a range into a view. |
| `std::ranges::ref_view` | Takes all elements of another range. |
| `std::ranges::owning_view` | Owns uniquely another range. |
| `std::ranges::iota_view`<br>`std::views::iota` | Generates a view of incremented values. |
| `std::ranges::single_view`<br>`std::views::single` | Owns a single value. |
| `std::ranges::empty_view`<br>`std::views::empty` | A view with no elements. |
| `std::ranges::basic_istream_view`<br>`std::ranges::istream_view` | Reads elements from a stream. |
| `std::ranges::filter_view`<br>`std::views::filter` | Takes the elements that satisfy the predicate. |
| `std::ranges::transform_view`<br>`std::views::transform` | Transforms each element. |
| `std::ranges::take_view`<br>`std::views::take` | Takes the first *n* elements of another view. |
| `std::ranges::take_while_view`<br>`std::views::take_while` | Takes the elements of another view as long as the predicate returns true. |
| `std::ranges::drop_view`<br>`std::views::drop` | Skips the first *n* elements of another view. |
| `std::ranges::drop_while_view`<br>`std::views::drop_while` | Skips the initial elements of another view until the predicate returns false. |
| `std::ranges::join_view`<br>`std::views::join` | Joins a view of ranges. |
| `std::ranges::split_view`<br>`std::views::split` | Splits a view by using a delimiter. |