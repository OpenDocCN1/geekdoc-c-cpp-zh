

## 观察结果

LVQ 执行的学习过程如图 5.6 和图 5.7 所示。从输出中我们发现，这些向量被分类为属于类别 4。

## 5.3 示例 3：使用 Kohonen SOM 网络进行字符识别

本示例的目标是将大量黑白矩形像素显示中的每一个识别为英文字母表中的 26 个大写字母之一。字符图像基于 20 种不同字体，并且这 20 种字体中的每个字母都经过随机扭曲，从而生成一个包含 20,000 个独特刺激的文件。每个刺激被转换为 16 个原始数值属性（统计矩和边缘计数），然后进行缩放，使其适合 0 到 15 的整数值范围。前 16000 项用于训练，所得模型用于预测其余 4000 项的字母类别。

![](img/d9a4cc12c48f7466f309cbd3c4549c73_202_0.png)

**图 5.6：** 输入格式

该程序中初始化的一些参数如下：

- 实例数量：20000
- 属性数量：17（字母类别和 16 个数值特征）
- 属性信息：
  - 1. `lettr` 大写字母（从 A 到 Z 的 26 个值）
  - 2. `position of box`（整数）
  - 3. `y-box` 框的垂直位置（整数）
  - 4. `width` 框的宽度（整数）
  - 5. `high` 框的高度（整数）
  - 6. `onpix` 亮像素总数（整数）
  - 7. `x-bar` 框内亮像素的 x 均值（整数）
  - 8. `y-bar` 框内亮像素的 y 均值（整数）
  - 9. `x2bar` x 方差均值（整数）
  - 10. `y2bar` y 方差均值（整数）
  - 11. `xybar` x 与 y 相关性的均值（整数）
  - 12. `x2ybr` x * x * y 的均值（整数）
  - 13. `xy2br` x * y * y 的均值（整数）
  - 14. `x-ege` 从左到右的边缘计数均值（整数）
  - 15. `xegvy` x-ege 与 y 的相关性（整数）
  - 16. `y-ege` 从下到上的边缘计数均值（整数）
  - 17. `yegvx` y-ege 与 x 的相关性（整数）

![](img/d9a4cc12c48f7466f309cbd3c4549c73_203_0.png)

**图 5.7：** 输出格式

缺失属性值：无

类别分布：

| 类别 | A | B | C | D | E | F | G | H |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 类别分布 | 789 | 766 | 736 | 805 | 768 | 775 | 773 | 734 |

| 类别 | I | J | K | L | M | N | O | P |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 类别分布 | 755 | 747 | 739 | 761 | 792 | 783 | 753 | 803 |

| 类别 | Q | R | S | T | U | V | W | X |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| 类别分布 | 783 | 758 | 748 | 796 | 813 | 764 | 752 | 787 |

| 类别 | Y | Z |
|---|---:|---:|
| 类别分布 | 786 | 734 |

```matlab
% MATLAB CODE
% ANALOG DATA

clear all;
clc;
m1 = 26;
alpha = input('Enter the value of alpha = ');
per1 = input('Enter the percentage of training vectors = ');
per2 = input('Enter the percentage of testing vectors = ');
x1 = load('d:\final\mqdata160rand.txt');
[patt n] = size(x1);
x2 = x1;
maxi = max(x1, [], 1);
value = x2(:, 1);

for j = 2:n
    x2(:, j-1) = x2(:, j) / maxi(j);
end

[pattern n] = size(input);
ci = 1;
for i = 1:m1
    while (i ~= value(ci))
        ci = ci + 1;
        if (ci > patt)
            ci = 1;
        end
    end
    w(i, :) = input(i, :);
    ci = 1;
end
countw = ones(1, m1);
alphacond = 0.000001 * alpha;
ep = 0;
patterntrain = round(pattern * per1 / 100);
for i = 1:patterntrain
    for j = 1:m1
        if (value(i) == j)
            countw(j) = countw(j) + 1;
            w(j, :) = ((countw(j) - 1) * w(j, :) + input(i, :)) / countw(j);
        end
    end
end
tic;
while (alpha > alphacond)
    clc;
    ep = ep + 1
    for p = 1:patterntrain
        data = input(p, :);
        for i = 1:m1
            d(i) = sum(power((w(i, :) - data(1, :)), 2));
        end
        [mind mini] = min(d);

        w(mini, :) = w(mini, :) + alpha * (data(1, :) - w(mini, :));
    end
    alpha = alpha * 0.9;
end
t = toc;
count = 0;
patterntest = round(pattern * per2 / 100);
for p = 1:patterntest
    data = input(p, :);
    for i = 1:m1
        d(i) = sum(power((w(i, :) - data(1, :)), 2));
    end
    [mind mini] = min(d);
    output(p) = mini;
    if (mini == value(p))
        count = count + 1;
    end
end
fprintf('\nPercentage of TRAINING Vectors : %f', per1);
fprintf('\nPercentage of TESTING Vectors : %f', per2);
fprintf('\nTime Taken for TRAINING : %f in secs', t);

eff = count * 100 / patterntest;
fprintf('\nEfficiency = %f', eff);
```

**表 5.2：** 模拟数据的结果

| 训练向量 | 测试向量 | 时间（秒） | 效率（%） |
|---:|---:|---:|---:|
| 20 | 80 | 2.01 | 51.56 |
| 40 | 60 | 3.98 | 73.95 |
| 60 | 40 | 5.78 | 89.06 |
| 80 | 20 | 9.23 | 93.75 |
| 95 | 5 | 9.36 | 100 |

```matlab
% DIGITAL DATA

clear all;
clc;
m1 = 26;
alpha = input('Enter the value of alpha = ');
per1 = input('Enter the percentage of training vectors ');
per2 = input('Enter the percentage of testing vectors ');
x1 = load('d:\finalpgm\data160rand.txt');
[patt n] = size(x1);
x2 = x1;
maxi = max(x1, [], 1);
value = x2(:, 1);

for j = 2:n
    input(:, (j-1)) = x2(:, j) / maxi(j);
end
[pattern n] = size(input);
for i = 1:pattern
    for j = 1:16
        if (input(i, j) > 0.5)
            input(i, j) = 1;
        else
            input(i, j) = 0;
        end
    end
end
ci = 1;
for i = 1:m1
    while (i ~= value(ci))
        ci = ci + 1;
        if (ci > patt)
            ci = 1;
        end
    end
    w(i, :) = input(i, :);
    ci = 1;
end
countw = ones(1, m1);
alphacond = 0.000001 * alpha;

ep = 0;
patterntrain = round(pattern * per1 / 100);
for i = 1:patterntrain
    for j = 1:m1
        if (value(i) == j)
            countw(j) = countw(j) + 1;
            w(j, :) = ((countw(j) - 1) * w(j, :) + input(i, :)) / countw(j);
        end
    end
end
tic;

while (alpha > alphacond)
    clc;
    ep = ep + 1
    for p = 1:patterntrain
        data = input(p, :);
        for i = 1:m1
            d(i) = sum(power((w(i, :) - data(1, :)), 2));
        end
        [mind mini] = min(d);
        w(mini, :) = w(mini, :) + alpha * (data(1, :) - w(mini, :));
    end
    alpha = alpha * 0.9;
end
t = toc;
count = 0;
patterntest = round(pattern * per2 / 100);
for p = 1:patterntest
    data = input(p, :);
    for i = 1:m1
        d(i) = sum(power((w(i, :) - data(1, :)), 2));
    end
    [mind mini] = min(d);
    output(p) = mini;
    if (mini == value(p))
        count = count + 1;
    end
end

% RESULTS:
fprintf('\nPercentage of TRAINING Vectors : %f', per1);
fprintf('\nPercentage of TEST Vectors : %f', per2);
fprintf('\nTime Taken for TRAINING : %f in secs', t);

eff = count * 100 / patterntest;
fprintf('\nEfficiency = %f', eff);
```

## 观察结果

表 5.2 和表 5.3 展示了 Kohonen 在模拟输入和数字输入下具有最优效率的结果。由此可以推断，效率随着训练向量数量的增加而提高。

**表 5.3：** 数字数据的结果

| 训练向量 | 测试向量 | 时间（秒） | 效率（%） |
|---:|---:|---:|---:|
| 20 | 80 | 1.98 | 70.31 |
| 40 | 60 | 3.87 | 79.16 |
| 60 | 40 | 6.03 | 82.81 |
| 80 | 20 | 7.76 | 84.37 |
| 95 | 5 | 9.29 | 100 |

