```
```cpp
auto max_sum = std::get<0>(sum_start_end);

auto start_index =
    std::distance(std::begin(a),
                  std::get<1>(sum_start_end));

auto end_index =
    std::distance(std::begin(a),
                  std::get<2>(sum_start_end));

std::cout << "sum: " << max_sum << ", "
          << ", start_index: " << start_index << ", "
          << ", end_index: " << end_index << ">"
          << "\nMax subarray is: ";

printcontents(std::get<1>(sum_start_end),
              std::get<2>(sum_start_end));

std::vector<int> v
{-1, 4, -2, 5, -5, 2, -20, 6};

typedef std::vector<int>::iterator vitr;
std::tuple<int, vitr, vitr>
    sum_start_end_v;
sum_start_end_v =
    kadane1(v.begin(), v.end());

max_sum = std::get<0>(sum_start_end_v);

start_index =
    std::distance(v.begin(),
                  std::get<1>(sum_start_end_v));

end_index = std::distance(v.begin(),
                          std::get<2>(sum_start_end_v));

std::cout << "sum: " << max_sum << ", "
          << ", start_index: " << start_index << ", "
          << ", end_index: " << end_index << ">"
          << "\nMax subarray is: ";

printcontents(std::get<1>(sum_start_end_v),
              std::get<2>(sum_start_end_v));

std::forward_list<int> l
{-2, 1, -3, 4, -1, 2, 1, -5, 4};

typedef std::forward_list<int>::iterator
    litr;
std::tuple<int, litr, litr> sum_start_end_l;
sum_start_end_l =
    kadane1(l.begin(), l.end());
```
```