```
```cpp
SingleValue singleValue0;
SingleValue singleValue2020{2020};
SingleValue singleValue2023{2023};


std::cout << std::format("{:*<10}", singleValue0) << '\n';
std::cout << std::format("{:*>10}", singleValue2020) << '\n';
std::cout << std::format("{:*^10}", singleValue2023) << '\n';


std::cout << '\n';
}
```
```

std::formatter<SingleValue> (line 17) has a standard formatter for int: std::formatter<int> formatter (line 20). I delegate the parsing job (line 23) to the formatter (line 23). Accordingly, the formatting job format is also delegated to the formatter (line 27).

The program's output shows that the formatter supports fill characters and alignment.

![](bbox=[0.2, 0.51, 0.75, 0.66])

# ### 5.5.3.1.3 Inheritance

Thanks to inheritance, implementing the formatter for the user-defined type SingleValue is a piece of cake.