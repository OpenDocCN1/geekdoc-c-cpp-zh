```
```cpp
std::size_t count{};

public:
  TrimByView() = default;

  constexpr TrimByView(Range r, std::size_t cnt): range_(std::move(r)),
                                     begin_(std::ranges::begin(r)), end_(std::end(r)),
                                     count(cnt) {}

  constexpr auto begin() const {
    return begin_ + count;
  }
  constexpr auto end() const {
    return end_ - count;
  }
};

template<typename Range>
TrimByView(Range&& range, std::size_t& cnt) ->
                         TrimByView<std::ranges::views::all_t<Range>>;

int main() {

  std::vector<int> myVec{1, 2, 3, 4, 5, 6, 7, 8, 9};

  auto myTrimByView1 = TrimByView(myVec, 1);
  for (auto c : myTrimByView1) std::cout << c << " ";
  std::cout << '\n';

  for (auto i : std::views::reverse(TrimByView(myVec, 2))) std::cout << i << ' ';
  std::cout << '\n';

  for (auto i : TrimByView(myVec, 3) | std::views::reverse) std::cout << i << ' ';
  std::cout << '\n';

  std::cout << '\n';

  std::string myStr = "Only for testing purpose ";

  auto myTrimByView2 = TrimByView(myStr, 1);
  for (auto c: myTrimByView2) std::cout << c << " ";
  std::cout << '\n';

  for (auto i : std::views::reverse(TrimByView(myStr, 2))) std::cout << i << ' ';
  std::cout << '\n';
```
```