
```
CGFloat freeSpaceHeight = applicationFrame.size.height -
    keyboardBounds.size.height;

//---calculate how much the scrollview must scroll---
CGFloat scrollAmount = viewCenterY - freeSpaceHeight / 2.0;

if (scrollAmount < 0) scrollAmount = 0;

//---set the new scrollView contentSize---
scrollView.contentSize = CGSizeMake(
    applicationFrame.size.width,
    applicationFrame.size.height +
    keyboardBounds.size.height);

//---scroll the ScrollView---
[scrollView setContentOffset:CGPointMake(0, scrollAmount) animated:YES];
}
```

当 TextField 视图放弃其 First Responder 状态时，`textFieldDidEndEditing:` 方法将被调用。此时，你将 ScrollView 视图恢复到其原始内容大小：

//---when a TextField view is done editing---
-(void) textFieldDidEndEditing:(UITextField *) textFieldView {
    [UIView beginAnimations:@"back to original size" context:nil];
    scrollView.contentSize = scrollViewOriginalSize;
    [UIView commitAnimations];
}
```

这里需要强调的一个要点是，你使用 `UIView` 类的 `beginAnimations` 方法来在恢复到原始大小的过程中为 ScrollView 视图设置动画。如果不使用此方法，ScrollView 将非常突然地恢复到原始大小，导致闪烁。

键盘消失之前，`keyboardWillHide:` 方法将被调用。在这种情况下，你无需做太多事情：

//---when the keyboard disappears---
-(void)keyboardWillHide:(NSNotification *) notification
{
}
```

最后，在 `dealloc` 方法中，你释放所有已创建的 outlet：

```
-(void) dealloc {
    [textField release];
    [scrollView release];
    [super dealloc];
}
```

## 1.2 矩阵的运算

本节介绍矩阵的加法、减法、乘法和转置等运算，以及它们所满足的运算规律。

### 一、矩阵的加法与减法

定义1 设 $A=(a_{ij})_{m\times n}$ 与 $B=(b_{ij})_{m\times n}$ 是两个 $m\times n$ 矩阵，则 $A$ 与 $B$ 的和（差）定义为：

$$A \pm B = (a_{ij} \pm b_{ij})_{m\times n}$$

即两个同型矩阵相加（减），就是将它们的对应元素相加（减）。矩阵的加法满足以下运算规律（设 $A,B,C$ 均为 $m\times n$ 矩阵）：

- 1. 交换律：$A+B=B+A$；
- 2. 结合律：$(A+B)+C=A+(B+C)$；
- 3. 零矩阵的运算：$A+0=A$，$A+(-A)=0$。

其中 $0$ 表示零矩阵，$-A=(-a_{ij})$ 称为 $A$ 的负矩阵。

### 二、数与矩阵的乘法

定义2 设 $\lambda$ 是一个数，$A=(a_{ij})_{m\times n}$ 是一个矩阵，则数 $\lambda$ 与矩阵 $A$ 的乘积定义为：

$$\lambda A = (\lambda a_{ij})_{m\times n}$$

即数与矩阵相乘，就是用该数乘以矩阵的每一个元素。数与矩阵的乘法满足以下运算规律（设 $\lambda,\mu$ 为任意数，$A,B$ 为同型矩阵）：

- 1. 数乘结合律：$\lambda(\mu A)=(\lambda\mu)A$；
- 2. 数乘分配律：$(\lambda+\mu)A=\lambda A+\mu A$，$\lambda(A+B)=\lambda A+\lambda B$。

矩阵的加法与数乘统称为矩阵的线性运算。

### 三、矩阵的乘法

定义3 设 $A=(a_{ij})_{m\times s}$，$B=(b_{ij})_{s\times n}$，则 $A$ 与 $B$ 的乘积 $C=(c_{ij})_{m\times n}$ 定义为：

$$c_{ij} = \sum_{k=1}^{s} a_{ik} b_{kj} = a_{i1}b_{1j} + a_{i2}b_{2j} + \cdots + a_{is}b_{sj}$$

其中 $i=1,2,\cdots,m$；$j=1,2,\cdots,n$。即矩阵 $A$ 的第 $i$ 行与矩阵 $B$ 的第 $j$ 列对应元素乘积之和。

只有左矩阵的列数等于右矩阵的行数时，两个矩阵才能相乘。矩阵的乘法满足以下运算规律（假设下列运算均有意义）：

- 1. 结合律：$(AB)C=A(BC)$；
- 2. 左分配律：$A(B+C)=AB+AC$；
- 3. 右分配律：$(B+C)A=BA+CA$；
- 4. 数乘结合律：$(\lambda A)B = A(\lambda B)=\lambda(AB)$。

注意：矩阵乘法一般不满足交换律，即 $AB \neq BA$。

### 四、矩阵的转置

定义4 将矩阵 $A=(a_{ij})_{m\times n}$ 的行与列互换（行列互换）得到的新矩阵称为矩阵 $A$ 的转置矩阵，记为 $A^T$，即：

$$A^T = (a_{ji})_{n\times m}$$

矩阵的转置满足以下运算规律：

- 1. $(A^T)^T=A$；
- 2. $(A+B)^T=A^T+B^T$；
- 3. $(\lambda A)^T=\lambda A^T$；
- 4. $(AB)^T=B^T A^T$。

例 1 已知矩阵 $A = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix}$，$B = \begin{pmatrix} -1 & 0 \\ 1 & 2 \\ 1 & 1 \end{pmatrix}$，求 $AB$ 和 $BA$。

解 因为 $A$ 是 $2\times 3$ 矩阵，$B$ 是 $3\times 2$ 矩阵，所以 $AB$ 有意义，且为 $2\times 2$ 矩阵：

$$AB = \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix} \begin{pmatrix} -1 & 0 \\ 1 & 2 \\ 1 & 1 \end{pmatrix} = \begin{pmatrix} 4 & 7 \\ 7 & 16 \end{pmatrix}$$

而 $BA$ 是 $3\times 3$ 矩阵：

$$BA = \begin{pmatrix} -1 & 0 \\ 1 & 2 \\ 1 & 1 \end{pmatrix} \begin{pmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{pmatrix} = \begin{pmatrix} -1 & -2 & -3 \\ 9 & 12 & 15 \\ 5 & 7 & 9 \end{pmatrix}$$

![](img/16991b58db5894715c4a443315e06a22_172_0.png)

## 屏幕旋转

### 本章将学习的内容

- 如何支持四种不同的屏幕方向
- 设备旋转时触发的各种事件
- 如何在设备方向改变时重新定位 View 上的视图
- 如何在运行时动态更改屏幕旋转
- 如何在应用程序加载之前设置其方向

在第 2 章的 Hello World! 应用程序中，你看到了如何编写 iPhone 应用程序以便支持纵向或横向模式的查看。本章将更深入地探讨屏幕方向主题。特别是，你将学习如何在设备旋转时管理应用程序的方向。你还将学习如何在设备旋转时重新定位视图，以便应用程序能够利用屏幕尺寸的变化。

### 响应设备旋转

现代移动设备支持的一项功能是能够检测设备的当前方向——纵向或横向。应用程序可以利用此功能重新调整设备的屏幕，以最大化对新方向的使用。一个很好的例子是 iPhone 上的 Safari。当你将设备旋转到横向方向时，Safari 会自动旋转其视图，以便你拥有更宽的屏幕来查看页面内容（见图 6-1）。

这意味着你的应用程序将仅以横向模式显示（见图 6-3），Home 按钮在其左侧（因此常量的名称为 `UIInterfaceOrientationLandscapeLeft`）。

![](img/16991b58db5894715c4a443315e06a22_175_0.png)

图 6-3

如果用户将设备旋转到纵向模式或 Home 按钮在右侧的横向模式（`UIInterfaceOrientationLandscapeRight`），应用程序将不会改变其方向（见图 6-4）。

![](img/16991b58db5894715c4a443315e06a22_175_1.png)

图 6-4

> 注意 这是区分 `UIInterfaceOrientationLandscapeLeft` 和 `UIInterfaceOrientationLandscapeRight` 的一个简单方法。只需记住 `UIInterfaceOrientationLandscapeLeft` 指的是 Home 按钮位于左侧，而 `UIInterfaceOrientationLandscapeRight` 指的是 Home 按钮位于右侧。

### 不同类型的屏幕方向

到目前为止，你已经看到了一些与屏幕方向相关的常量：`UIInterfaceOrientationPortrait`、`UIInterfaceOrientationLandscapeLeft` 和 `UIInterfaceOrientationLandscapeRight`。你总共有四个常量可用于指定屏幕方向：

- `UIInterfaceOrientationPortrait` — 以纵向模式显示屏幕
- `UIInterfaceOrientationPortraitUpsideDown` — 以纵向模式显示屏幕，但 Home 按钮位于屏幕顶部
- `UIInterfaceOrientationLandscapeLeft` — 以横向模式显示屏幕，Home 按钮在左侧
- `UIInterfaceOrientationLandscapeRight` — 以横向模式显示屏幕，Home 按钮在右侧

![](img/16991b58db5894715c4a443315e06a22_176_0.png)

在四种模式中，通常不建议使用 `UIInterfaceOrientationPortraitUpsideDown` 模式，因为它很容易使你的用户感到迷失方向（见图 6-5）。

如果你的应用程序支持多种屏幕方向，你应该重写 `shouldAutorotateToInterfaceOrientation:` 方法，然后使用 `||`（逻辑或）运算符来指定它支持的所有方向，像这样：

```
- (BOOL)shouldAutorotateToInterfaceOrientation:
    (UIInterfaceOrientation)interfaceOrientation {

    return (interfaceOrientation == UIInterfaceOrientationPortrait ||
            interfaceOrientation == UIInterfaceOrientationLandscapeRight);
}
```

前面的代码片段使你的应用程序能够同时支持纵向和横向右侧模式。

### 处理旋转

iPhone SDK 视图控制器在屏幕旋转期间公开了几个你可以处理的事件。能够处理旋转期间触发的事件很重要，因为它允许你重新定位 View 上的视图，或者在屏幕旋转时停止媒体播放。你可以处理的事件有：

- willAnimateFirstHalfOfRotationToInterfaceOrientation:
- willAnimateSecondHalfOfRotationFromInterfaceOrientation:
- willRotateToInterfaceOrientation:
- willAnimateRotationToInterfaceOrientation:

以下各节更详细地介绍这些事件中的每一个。

#### willAnimateFirstHalfOfRotationToInterfaceOrientation:

首先，`willAnimateFirstHalfOfRotationToInterfaceOrientation:` 事件在 View 开始旋转之前触发。该方法如下所示：

```
- (void)willAnimateFirstHalfOfRotationToInterfaceOrientation:
(UIInterfaceOrientation) toInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```

`toInterfaceOrientation` 参数指示 View 正在更改到的方向，而 `duration` 参数指示旋转第一半的持续时间，以秒为单位。

在此事件中，你可以插入代码以在旋转开始之前执行你想要执行的任务，例如暂停媒体播放、暂停动画等。

#### willAnimateSecondHalfOfRotationFromInterfaceOrientation:

`willAnimateSecondHalfOfRotationFromInterfaceOrientation:` 事件在旋转进行到一半时触发（见图 6-6）。该方法如下所示：

```
- (void)willAnimateSecondHalfOfRotationFromInterfaceOrientation:
(UIInterfaceOrientation) fromInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```
