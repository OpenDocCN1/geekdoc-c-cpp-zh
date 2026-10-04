

```cpp
std::cout << "输入第二个矩阵的元素：\n";
for (int i = 0; i < rows2; i++) {
  for (int j = 0; j < cols2; j++) {
    std::cin >> matrix2[i][j];
  }
}
```

```cpp
// 检查是否可以乘
if (cols1 != rows2) {
  std::cout << "矩阵无法相乘...";
  return 0;
}
```

```cpp
// 执行乘法
std::vector<std::vector<double>> result(rows1, std::vector<double>(cols2, 0));
for (int i = 0; i < rows1; i++) {
  for (int j = 0; j < cols2; j++) {
    for (int k = 0; k < cols1; k++) {
      result[i][j] += matrix1[i][k] * matrix2[k][j];
    }
  }
}
```

```cpp
}
}
// 显示结果
std::cout << "矩阵乘法的结果：\n";
for (int i = 0; i < rows1; i++) {
    for (int j = 0; j < cols2; j++) {
        std::cout << result[i][j] << " ";
    }
    std::cout << "\n";
}
```

return 0;
}
```

## 133. 螺旋顺序打印一个矩阵。

```cpp
#include <iostream>
#include <vector>

int main() {
    int rows, cols;

// 读取矩阵维度
std::cout << "输入行数和列数：";
std::cin >> rows >> cols;

// 读取矩阵值
std::vector<std::vector<int>> matrix(rows, std::vector<int>(cols));
std::cout << "输入矩阵：\n";
for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
        std::cin >> matrix[i][j];
    }
}

int top = 0, bottom = rows - 1, left = 0, right = cols - 1;

// 螺旋顺序打印矩阵
while (top <= bottom && left <= right) {
    // 打印顶行
    for (int i = top; i <= right; i++) {
        std::cout << matrix[top][i] << " ";
    }
    top++;

    // 打印最右侧列
    for (int i = top; i <= bottom; i++) {
        std::cout << matrix[i][right] << " ";
    }
    right--;

    // 打印底行（如果还有行需要处理）
    if (top <= bottom) {
        for (int i = right; i >= left; i--) {
            std::cout << matrix[bottom][i] << " ";
        }
        bottom--;
    }

    // 打印最左侧列（如果还有列需要处理）
    if (left <= right) {
        for (int i = bottom; i >= top; i--) {
            std::cout << matrix[i][left] << " ";
        }
        left++;
    }
}
return 0;
}
```

## 134. 一个一个程序读取 m x n 矩阵，用 0 表示中立区域，1 表示地雷位置，该程序应返回一个矩阵，标明每个位置相邻房屋中的地雷数量。

```cpp
#include <iostream>
#include <vector>

int main() {
    int m, n;
    // 读取矩阵维度
    std::cout << "输入行数和列数： ";
    std::cin >> m >> n;

    // 读取矩阵值
    std::vector<std::vector<int>> matrix(m, std::vector<int>(n));
    std::cout << "输入元素（0 表示中立，1 表示地雷）：\n";
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            std::cin >> matrix[i][j];
        }
    }

    std::vector<std::vector<int>> result(m, std::vector<int>(n, 0));
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            // 如果该位置有地雷，跳过计数
            if (matrix[i][j] == 1) continue;

            // 检查 8 个单元格
            for (int x = -1; x <= 1; x++) {
                for (int y = -1; y <= 1; y++) {
                    if (x == 0 && y == 0) continue; // 跳过当前单元格
                    int new_i = i + x;
                    int new_j = j + y;

                    if (new_i >= 0 && new_i < m && new_j >= 0 && new_j < n && matrix[new_i][new_j] == 1) {
                        result[i][j]++;
                    }
                }
            }
        }
    }

    // 输出结果矩阵
    std::cout << "结果矩阵：\n";
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == 1)
                std::cout << "M ";
            else
                std::cout << result[i][j] << " ";
        }
        std::cout << "\n";
    }

    return 0;
}
```

## 135. 编写一个函数接收一个代表井井棋游戏的 3x3 矩阵，并检查是否有胜者、是否平局或游戏尚未结束。

```cpp
#include <iostream>
#include <vector>

enum class GameState {
    X_Wins,
    O_Wins,
    Tie,
    Ongoing
};

GameState checkTicTacToe(std::vector<std::vector<char>>& board) {
    // 检查行、列、对角线
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2]) {
            return board[i][0] == 'X' ? GameState::X_Wins : GameState::O_Wins;
        }
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i]) {
            return board[0][i] == 'X' ? GameState::X_Wins : GameState::O_Wins;
        }
    }
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2]) {
        return board[0][0] == 'X' ? GameState::X_Wins : GameState::O_Wins;
    }
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0]) {
        return board[0][2] == 'X' ? GameState::X_Wins : GameState::O_Wins;
    }

    bool tie = true;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ') {
                tie = false;
                break;
            }
        }
    }
    return tie ? GameState::Tie : GameState::Ongoing;
}
```

## 136. 编写一个计算数字阶乘的递归函数。

```cpp
#include <iostream>
long long factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n - 1);
}

int main() {
    int num;
    std::cout << "输入数字：";
    std::cin >> num;
    std::cout << num << " 的阶乘是 " << factorial(num) << std::endl;
    return 0;
}
```

## 137. 实现一个递归函数计算到某项的斐波那契序列。

```cpp
#include <iostream>
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int num;
    std::cout << "输入项数：";
    std::cin >> num;
    std::cout << "前 " << num << "项斐波那契序列：" << std::endl;
    for (int i = 0; i < num; i++) {
        std::cout << fibonacci(i) << " ";
    }
    std::cout << std::endl;
    return 0;
}
```

## 138. 创建一个递归函数检查数字是否为质数。

```cpp
#include <iostream>
bool isPrimeRecursive(int n, int i = 2) {
    if (n <= 1) return false;
    if (n % i == 0) return false;
    if (i * i > n) return true;
    return isPrimeRecursive(n, i + 1);
}

int main() {
    int num;
    std::cout << "输入数字：";
    std::cin >> num;
    if (isPrimeRecursive(num)) {
        std::cout << num << " 是质数。" << std::endl;
    } else {
        std::cout << num << "不是质数。" << std::endl;
    }
    return 0;
}
```

## 139. 开发一个递归函数计算整数各位数字之和。

```cpp
#include <iostream>
int sumOfDigits(int n) {
  if (n < 10) return n;
  return n % 10 + sumOfDigits(n / 10);
}

int main() {
  int num;
  std::cout << "输入数字：";
  std::cin >> num;
  std::cout << "数字之和：" << sumOfDigits(num) << std::endl;
  return 0;
}
```

