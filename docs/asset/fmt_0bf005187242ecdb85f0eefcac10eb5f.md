
```cpp
#include <iostream>
#include <cmath> // 使用 pow() 函数

int main() {
    double base, exponent;

    // 提示用户输入底数的指数
    std::cout << "Enter the base: ";
    std::cin >> base;

    std::cout << "Enter the exponent: ";
    std::cin >> exponent;

    // 计算幂
    double result = std::pow(base, exponent);

    // 显示结果
    std::cout << base << " raised to the power of " << exponent << " is: " << result << std::endl;

    return 0;
}
```

## 15. 写一个程序，读取一个数字并在屏幕上打印该数字的平方根。

```cpp
#include <iostream>
#include <cmath> // 使用 sqrt() 函数

int main() {
    double number;

    // 提示用户输入一个数字
    std::cout << "Enter a number: ";
    std::cin >> number;

    // 确保数字非负
    if (number < 0) {
        std::cout << "The number is negative, and its square root is not real." << std::endl;
        return 1;
    }

    // 使用 sqrt() 函数计算平方根
    double sqrt_value = std::sqrt(number);

    // 显示结果
    std::cout << "The square root of " << number << " is: " << sqrt_value << std::endl;

    return 0;
}
```

# 16. 写一个程序，计算用户输入的三个数字的几何平均值 -> GeoMean = $\sqrt[3]{n_1 \times n_2 \times n_3}$

```cpp
#include <iostream>
#include <cmath> // 使用 cbrt() 和 pow() 函数

int main() {
    double num1, num2, num3;

    // 提示用户输入三个数字
    std::cout << "Enter the first number: ";
    std::cin >> num1;

    std::cout << "Enter the second number: ";
    std::cin >> num2;

    std::cout << "Enter the third number: ";
    std::cin >> num3;

    // 计算几何平均值
    double product = num1 * num2 * num3;
    double geometric_mean = std::cbrt(product);
    // 或者，你可以使用 pow() 函数
    // double geometric_mean = std::pow(product, 1.0 / 3.0);

    return 0;
}
```

## 17. 写一个程序，计算个人的 BMI，使用公式 BMI = weight / height²

```cpp
#include <iostream>
#include <cmath> // 使用 pow()

int main() {
    double weight, height;

    // 提示用户输入体重和身高
    std::cout << "Enter your weight in kilograms: ";
    std::cin >> weight;

    std::cout << "Enter your height in meters: ";
    std::cin >> height;

    // 计算 BMI
    double bmi = weight / std::pow(height, 2);

    // 显示 BMI
    std::cout << "Your BMI is: " << bmi << std::endl;

    return 0;
}
```

## 18. 创建一个程序，计算并显示圆的周长，提示用户输入半径，使用公式 P = 2πr

```cpp
#include <iostream>
#include <cmath> // 使用 M_PI 常量

int main() {
    double radius;

    // 提示用户输入半径
    std::cout << "Enter the radius of the circle: ";
    std::cin >> radius;

    // 计算周长
    double perimeter = 2 * M_PI * radius;

    // 显示结果
    std::cout << "The perimeter (circumference) of the circle with radius " << radius << " is: " << perimeter << std::endl;

    return 0;
}
```

```cpp
perimeter << std::endl;

return 0;
}
```

# 19. 写一个程序，根据半径使用公式 A = πr² 计算圆的面积

```cpp
#include <iostream>
#include <cmath> // 用于 M_PI 常量

int main() {
    double radius;

    // 提示用户输入半径
    std::cout << "Enter the radius of the circle: ";
    std::cin >> radius;

    // 计算面积
    double area = M_PI * std::pow(radius, 2);

    // 显示结果
    std::cout << "The area of the circle with radius " << radius << " is:" << area << std::endl;

    return 0;
}
```

## 20. 写一个程序，计算一元方程的判别式（Δ = b² - 4ac）。

```cpp
#include <iostream>
#include <cmath>

int main() {
    double a, b, c;

    // 提示用户输入二次方程的系数
    std::cout << "Enter the coefficient a: ";
    std::cin >> a;

    std::cout << "Enter the coefficient b: ";
    std::cin >> b;

    std::cout << "Enter the coefficient c: ";
    std::cin >> c;

    // 计算判别式 (Δ)
    double delta = std::pow(b, 2) - 4 * a * c;

    // 显示结果
    std::cout << "The delta (Δ) of the equation is: " << delta << std::endl;

    return 0;
}
```

# 21. 写一个程序，根据公式 P = 2(w + l) 和 A = wl 计算矩形的周长和面积，其中 w 是宽，l 是长

```cpp
#include <iostream>

int main() {
    double width, length;

    // 提示用户输入矩形的宽和长
    std::cout << "Enter the width of the rectangle: ";
    std::cin >> width;

    std::cout << "Enter the length of the rectangle: ";
    std::cin >> length;

    // 计算周长和面积
    double perimeter = 2 * (width + length);
    double area = width * length;

    // 显示结果
    std::cout << "The perimeter of the rectangle is: " << perimeter << std::endl;
    std::cout << "The area of the rectangle is: " << area << std::endl;

    return 0;
}
```

# 22. 写一个程序，根据公式 P = a + b + c 和 A = (b * h) / 2 计算三角形的周长和面积，其中 a, b 和 c 是三角形的边，h 是对应边 b 的高。

```cpp
#include <iostream>

int main() {
    double a, b, c, h;

    // 提示用户输入三角形的边和高
    std::cout << "Enter the length of side a: ";
    std::cin >> a;

    std::cout << "Enter the length of side b: ";
    std::cin >> b;

    std::cout << "Enter the length of side c: ";
    std::cin >> c;

    std::cout << "Enter the height relative to side b: ";
    std::cin >> h;

    // 计算周长和面积
    double perimeter = a + b + c;
    double area = (b * h) / 2;

    // 显示结果
    std::cout << "The perimeter of the triangle is: " << perimeter << std::endl;
    std::cout << "The area of the triangle is: " << area << std::endl;

    return 0;
}
```

# 23. 写一个程序，根据公式 v = Δs/Δt 计算物体的平均速度，其中 Δs 是位移，Δt 是时间间隔

```cpp
#include <iostream>

int main() {
    double delta_s, delta_t;

    // 提示用户输入位移和时间间隔
    std::cout << "Enter the space variation (Δs) in meters:";
    std::cin >> delta_s;

    std::cout << "Enter the time variation (Δt) in seconds:";
    std::cin >> delta_t;

    // 计算平均速度
    double average_velocity = delta_s / delta_t;

    // 显示结果
    std::cout << "The average velocity (v) is: " << average_velocity << " m/s";

    return 0;
}
```

# 24. 写一个程序，根据公式 E = mv² / 2 计算运动物体的动能，其中 m 是质量，v 是速度。

```cpp
#include <iostream>
#include <cmath> // 用于 pow()

int main() {
    double mass, velocity;

    // 提示用户输入物体的质量和速度
    std::cout << "Enter the mass of the object (in kg):";
    std::cin >> mass;

    std::cout << "Enter the velocity of the object (in m/s): ";
    std::cin >> velocity;

    // 计算动能
    double kinetic_energy = (mass * std::pow(velocity, 2)) / 2;

    // 显示结果
    std::cout << "The kinetic energy of the object is: " << kinetic_energy << " Joules";

    return 0;
}
```

# 25. 写一个程序，根据公式 W = F * d 计算作用于物体的力功，其中 F 是作用力，d 是位移。

```cpp
#include <iostream>

int main() {
    double force, distance;

    // 提示用户输入作用力和位移
    std::cout << "Enter the force applied on the object (Newtons):";
    std::cin >> force;

    std::cout << "Enter the distance traveled by the object (in meters):";
    std::cin >> distance;

    // 计算功
    double work = force * distance;

    // 显示结果
    std::cout << "The work done by the force is: " << work << " Joules";

    return 0;
}
```

# 26. 写一个程序，给定第一项、公差以及从用户输入的 n，计算等差数列的第 n 项，a_n = a_1 + (n - 1) * r

```cpp
#include <iostream>

int main() {
    double a1, d;
    int n;

    // 提示用户输入第一项、公差和 n
    std::cout << "Enter the first term of the arithmetic progression: ";
    std::cin >> a1;

    std::cout << "Enter the common difference of the arithmetic progression: ";
    std::cin >> d;

    std::cout << "Enter n:";
    std::cin >> n;

    // 计算第 n 项
    double a_n = a1 + (n - 1) * d;

    // 显示结果
    std::cout << "The n-th term of the arithmetic progression is: " << a_n << std::endl;

    return 0;
}
```

# 27. 写一个程序，读取笛卡尔平面上两个点的 x y 位置，并计算它们之间的距离

```cpp
#include <iostream>
#include <cmath> // 用于 sqrt() 和 pow() 函数

int main() {
    double x1, y1, x2, y2;

    // 提示用户输入第一个点的坐标
    std::cout << "Enter the x and y coordinates of the first point (separated by space): ";
    std::cin >> x1 >> y1;

    // 提示用户输入第二个点的坐标
    std::cout << "Enter the x and y coordinates of the second point (separated by space): ";
    std::cin >> x2 >> y2;

    // 计算两点间的距离
    double distance = sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2));

    // 显示结果
    std::cout << "The distance between the two points is: " << distance << std::endl;

    return 0;
}
```

# 28. 创建一个程序，提示用户输入球体半径并计算且显示其体积。
