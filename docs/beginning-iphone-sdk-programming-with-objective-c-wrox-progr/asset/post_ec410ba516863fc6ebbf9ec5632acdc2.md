
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

When the TextField view resigns its First Responder status, the `textFieldDidEndEditing:` method will be invoked. At this point, you restore the ScrollView view to its original content size:

```
//---when a TextField view is done editing---
-(void) textFieldDidEndEditing:(UITextField *) textFieldView {
    [UIView beginAnimations:@"back to original size" context:nil];
    scrollView.contentSize = scrollViewOriginalSize;
    [UIView commitAnimations];
}
```

A noteworthy point to highlight here is that you use the `beginAnimations` method of the `UIView` class to animate the ScrollView view in the process of restoring to its original size. If you do not use this method, the ScrollView will very abruptly restore to its original size, causing a flicker.

Just before the keyboard disappears, the `keyboardWillHide:` method is invoked. In this case, you don't have much to do:

```
//---when the keyboard disappears---
-(void)keyboardWillHide:(NSNotification *) notification
{
}
```

Finally, in the `dealloc` method, you release all the outlets you have created:

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

## Screen Rotations

### WHAT YOU WILL LEARN IN THIS CHAPTER

- How to support the four different types of screen orientations
- The various events that are fired when a device rotates
- How to reposition the views on a View when the orientation of a device changes
- How to change the screen rotation dynamically during runtime
- How to set the orientation of your application before it is loaded

With the Hello World! application in Chapter 2, you saw how your iPhone application can be written so that it supports viewing in either the portrait or landscape mode. This chapter dives deeper into the topic of screen orientation. In particular, you will learn how to manage the orientation of your application when the device is rotated. You will also learn how to reposition your views when the device is rotated so that your application can take advantage of the change in screen dimensions.

### RESPONDING TO DEVICE ROTATIONS

One of the features that modern mobile devices support is the ability to detect the current orientation — portrait or landscape — of the device. An application can take advantage of this ability to readjust the device's screen to maximize the use of the new orientation. A good example is Safari on the iPhone. When you rotate the device to landscape orientation, Safari automatically rotates its view so that you have a wider screen to view the content of the page (see Figure 6-1).

This means that your application will display only in landscape mode (see Figure 6-3) with the Home button on its left (hence the constant name `UIInterfaceOrientationLandscapeLeft`).

![](img/16991b58db5894715c4a443315e06a22_175_0.png)

FIGURE 6-3

If the user rotates the device to portrait mode or landscape mode with the Home button on the right (`UIInterfaceOrientationLandscapeRight`), the application will not change its orientation (see Figure 6-4).

![](img/16991b58db5894715c4a443315e06a22_175_1.png)

FIGURE 6-4

> NOTE Here is one easy way to differentiate between `UIInterfaceOrientationLandscapeLeft` and `UIInterfaceOrientationLandscapeRight`. Just remember that `UIInterfaceOrientationLandscapeLeft` refers to the Home button positioned on the left and `UIInterfaceOrientationLandscapeRight` refers to the Home button positioned on the right.

### Different Types of Screen Orientations

So far, you have seen a few constants related to screen orientations: `UIInterfaceOrientationPortrait`, `UIInterfaceOrientationLandscapeLeft`, and `UIInterfaceOrientationLandscapeRight`. You have a total of four constants to use for specifying screen orientations:

- `UIInterfaceOrientationPortrait` — displays the screen in portrait mode
- `UIInterfaceOrientationPortraitUpsideDown` — displays the screen in portrait mode but with the Home button at the top of the screen
- `UIInterfaceOrientationLandscapeLeft` — displays the screen in landscape mode with the Home button on the left
- `UIInterfaceOrientationLandscapeRight` — displays the screen in landscape mode with the Home button on the right

![](img/16991b58db5894715c4a443315e06a22_176_0.png)

Of the four modes, it is usually not recommended to use the `UIInterfaceOrientationPortraitUpsideDown` mode because it could easily disorient your users (see Figure 6-5).

If your application supports multiple screen orientations, you should override the `shouldAutorotateToInterfaceOrientation:` method and then use the `||` (logical OR) operator to specify all the orientations it supports, like this:

```
- (BOOL)shouldAutorotateToInterfaceOrientation:
    (UIInterfaceOrientation)interfaceOrientation {

    return (interfaceOrientation == UIInterfaceOrientationPortrait ||
            interfaceOrientation == UIInterfaceOrientationLandscapeRight);
}
```

The preceding code snippet enables your application to support both the portrait and landscape-right modes.

### Handling Rotations

The iPhone SDK view controller exposes several events that you can handle during the rotation of the screen. The ability to handle events fired during rotation is important because it allows you to reposition the views on the View, or you can stop media playback while the screen is rotating. The events that you can handle are:

- willAnimateFirstHalfOfRotationToInterfaceOrientation:
- willAnimateSecondHalfOfRotationFromInterfaceOrientation:
- willRotateToInterfaceOrientation:
- willAnimateRotationToInterfaceOrientation:

The following sections take a more detailed look at each of these events.

#### willAnimateFirstHalfOfRotationToInterfaceOrientation:

First, the `willAnimateFirstHalfOfRotationToInterfaceOrientation:` event is fired just before the rotation of the View starts. The method looks like this:

```
- (void)willAnimateFirstHalfOfRotationToInterfaceOrientation:
(UIInterfaceOrientation) toInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```

The `toInterfaceOrientation` parameter indicates the orientation that the View is changing to, and the `duration` parameter indicates the duration of the first half of the rotation, in seconds.

In this event, you can insert your code to perform tasks that you want to perform before the rotation starts, such as pausing media playback, pausing animations, and so on.

#### willAnimateSecondHalfOfRotationFromInterfaceOrientation:

The `willAnimateSecondHalfOfRotationFromInterfaceOrientation:` event is fired when the rotation is halfway through (see Figure 6-6). The method looks like this:

```
- (void)willAnimateSecondHalfOfRotationFromInterfaceOrientation:
(UIInterfaceOrientation) fromInterfaceOrientation
 duration: (NSTimeInterval) duration {
}
```
