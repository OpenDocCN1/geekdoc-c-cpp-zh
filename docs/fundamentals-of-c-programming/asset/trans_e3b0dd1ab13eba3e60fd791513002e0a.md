

## 图 5.3 当用户提供 805 作为输入值时，二进制数转换程序的过程

![](img/e84ad11adb18201d71595b31ce6c9eff_116_0.png)

## 清单 5.11: simplerbinaryconversion.cpp

```cpp
#include <iostream>

int main() {
  int value;
  // Get number from the user
  std::cout << "Please enter an integer value in the range 0...1023: ";
  std::cin >> value;
  // Input value must be less than 1024
  if (0 <= value && value < 1024) {
    std::cout << value;
    value %= 512;
    std::cout << value << value/256;
    value %= 256;
    std::cout << value << value/128;
    value %= 128;
    std::cout << value << value/64;
    value %= 64;
    std::cout << value << value/32;
    value %= 32;
    std::cout << value << value/16;
    value %= 16;
    std::cout << value << value/8;
    value %= 8;
    std::cout << value << value/4;
    value %= 4;
    std::cout << value << value/2;
    value %= 2;
    std::cout << value << '\n';
  }
}
```

清单 5.11（simplerbinaryconversion.cpp）中唯一的 `if` 语句确保用户提供适当范围内的整数。最初出现在清单 5.10（binaryconversion.cpp）中的其他 `if` 语句已不再存在。一组巧妙的整数算术运算取代了原始的条件逻辑。这两个程序——binaryconversion.cpp 和 simplerbinaryconversion.cpp——行为相同，但 simplerbinaryconversion.cpp 的逻辑更简单。

清单 5.12（troubleshoot.cpp）实现了一个非常简单的故障排除程序，（同样简单的）计算机技术人员可以使用它来诊断故障计算机。

## 清单 5.12: troubleshoot.cpp

```cpp
#include <iostream>

int main() {
  std::cout << "Help! My computer doesn't work!\n";
  char choice;
  std::cout << "Does the computer make any sounds "
    << "(fans, etc.) or show any lights? (y/n): ";
  std::cin >> choice;
  // The troubleshooting control logic
  if (choice == 'n') { // The computer does not have power
    std::cout << "Is it plugged in? (y/n):";
    std::cin >> choice;
```

```cpp
if (choice == 'n') { // It is not plugged in, plug it in
    std::cout << "Plug it in. If the problem persists, "
              << "Please run this program again.\n";
}
else { // It is plugged in
    std::cout << "Is the switch in the \"on\" position? (y/n):";
    std::cin >> choice;
    if (choice == 'n') { // The switch is off, turn it on!
        std::cout << "Turn it on. If the problem persists, "
                  << "Please run this program again.\n";
    }
    else { // The switch is on
        std::cout << "Does the computer have a fuse? (y/n):";
        std::cin >> choice;
        if (choice == 'n') { // No fuse
            std::cout << "Is the outlet OK? (y/n):";
            std::cin >> choice;
            if (choice == 'n') { // Fix outlet
                std::cout << "Check the outlet's circuit "
                          << "breaker or fuse. Move to a "
                          << "new outlet, if necessary. "
                          << "If the problem persists, "
                          << "please run this program again.\n";
            }
            else { // Beats me!
                std::cout << "Please consult a service "
                          << "technician.\n";
            }
        }
        else { // Check fuse
            std::cout << "Check the fuse. Replace if "
                      << "necessary. If the problem "
                      << "persists, then "
                      << "please run this program again.\n";
        }
    }
} // The computer has power
else { // The computer has power
    std::cout << "Please consult a service technician.\n";
}
```
```

这个非常简单的故障排除程序试图诊断计算机无法工作的原因。改进的潜力是无限的，但此版本仅处理具有简单修复方法的电源问题。请注意，如果计算机有电源（风扇或磁盘驱动器发出声音或灯光可见），程序会指导用户去其他地方寻求帮助！捕获程序基本逻辑的决策树如图 5.4 所示。

执行的步骤如下：

- 1. 是否已插电？有时会忽略这个简单的修复方法。
- 2. 开关是否处于开启位置？这是另一个简单的修复方法。

## 图 5.4 计算机系统故障排除的决策树

![](img/e84ad11adb18201d71595b31ce6c9eff_119_0.png)

- 3. 如果适用，保险丝是否烧断？某些计算机系统具有用户可维护的保险丝，在电压浪涌时可能会烧断。（大多数较新的计算机具有可处理电压浪涌且没有用户可维护保险丝的电源。）
- 4. 插座处是否有电源？也许插座的断路器或保险丝有问题。

程序指导用户先进行较简单的检查。随着程序继续，它会逐步引入更困难的检查。根据你对无法正常运行的计算机进行故障排除的经验，你可能能够为这个简单的程序想出许多改进措施。

请注意，在清单 5.12（troubleshoot.cpp）中，花括号在许多严格来说不必要的地方被使用。在清单 5.12（troubleshoot.cpp）中加入它们可以提高程序的可读性，并使逻辑更易于理解。即使你不赞同为每个 if/else 体使用花括号的哲学，但在改善代码可读性的情况下使用它们也是个好主意。

回顾清单 4.11（timeconv.cpp）中的时间转换程序。如果用户输入 10000，程序运行如下：

```
Please enter the number of seconds:10000
2 hr 46 min 40 sec
```

如果用户输入 9961，程序打印：

```
Please enter the number of seconds:9961
2 hr 46 min 1 sec
```

假设我们希望通过不使用缩写来改进英文显示。如果我们拼写出 hours、minutes 和 seconds，则必须小心，在相应值为 1 时使用单数形式 hour、minute 或 second。清单 5.13（timeconvcond1.cpp）使用 if/else 语句以正确的数字表示时间单位。

## 清单 5.13: timeconvcond1.cpp

```cpp
// File timeconvcond1.cpp

#include <iostream>

int main( )
{
   // Some useful conversion constants
   const int SECONDS_PER_MINUTE = 60,
             SECONDS_PER_HOUR   = 60*SECONDS_PER_MINUTE; // 3600

   int hours, minutes, seconds;
   std::cout << "Please enter the number of seconds:";
   std::cin >> seconds;
   // First, compute the number of hours in the given number
   // of seconds
   hours = seconds / SECONDS_PER_HOUR; // 3600 seconds = 1 hours
   // Compute the remaining seconds after the hours are
   // accounted for
   seconds = seconds % SECONDS_PER_HOUR;
   // Next, compute the number of minutes in the remaining
   // number of seconds
   minutes = seconds / SECONDS_PER_MINUTE; // 60 seconds = 1 minute
   // Compute the remaining seconds after the minutes are
   // accounted for
   seconds = seconds % SECONDS_PER_MINUTE;
   // Report the results
   std::cout << hours;
   // Decide between singular and plural form of hours
   if (hours == 1)
      std::cout << " hour ";
   else
      std::cout << " hours ";
   std::cout << minutes;
   // Decide between singular and plural form of minutes
   if (minutes == 1)
      std::cout << " minute ";
   else
      std::cout << " minutes ";
   std::cout << seconds;
   // Decide between singular and plural form of seconds
   if (seconds == 1)
      std::cout << " second";
   else
      std::cout << " seconds";
   std::cout << '\n';
}
```

清单 5.13（timeconvcond1.cpp）中的 if/else 语句负责为每个时间单位打印正确的版本——单数或复数。清单 5.13（timeconvcond1.cpp）的一次运行产生

```
Please enter the number of seconds:10000
2 hours 46 minutes 40 seconds
```

所有单词都是复数，因为所有值都大于 1。另一次运行产生

```
Please enter the number of seconds:9961
2 hours 46 minutes 1 second
```

请注意，单词 second 是单数，正如它应该的那样。

```
Please enter the number of seconds:3601
1 hour 0 minutes 1 second
```

同样，此处打印的单词与它们所代表的值的数量一致。

对清单 5.13（timeconvcond1.cpp）的一个改进是：如果值为零，则不打印该值及其关联的时间单位。清单 5.14（timeconvcond2.cpp）添加了此功能。

## 清单 5.14: timeconvcond2.cpp

```cpp
// File timeconvcond1.cpp

#include <iostream>

int main() {
    // Some useful conversion constants
    // const int SECONDS_PER_MINUTE = 60,
    //             SECONDS_PER_HOUR   = 60*SECONDS_PER_MINUTE; // 3600

    int hours, minutes, seconds;
    std::cout << "Please enter the number of seconds:";
    std::cin >> seconds;
    // First, compute the number of hours in the given number
    // of seconds
    hours = seconds / SECONDS_PER_HOUR; // 3600 seconds = 1 hours
    // Compute the remaining seconds after the hours are
    // accounted for
    seconds = seconds % SECONDS_PER_HOUR;
    // Next, compute the number of minutes in the remaining
    // number of seconds
    minutes = seconds / SECONDS_PER_MINUTE; // 60 seconds = 1 minute
    // Compute the remaining seconds after the minutes are
    // accounted for
    seconds = seconds % SECONDS_PER_MINUTE;
    // Report the results
    if (hours > 0) { // Print hours at all?
        std::cout << hours;
        // Decide between singular and plural form of hours
        if (hours == 1)
            std::cout << " hour ";
        else
            std::cout << " hours ";
    }
    if (minutes > 0) { // Print minutes at all?
        std::cout << minutes;
        // Decide between singular and plural form of minutes
```

