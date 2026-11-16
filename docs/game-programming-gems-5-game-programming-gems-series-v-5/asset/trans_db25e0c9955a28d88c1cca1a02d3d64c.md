

运动。为了补偿，关于被跟随对象实际位置的预测提前0.7秒进行。因此，存储外推位置的样本缓冲区需要存储最后0.7秒的样本，在恒定帧率的情况下这很容易解决。然而，计算机游戏的帧率始终在变化，取决于渲染场景的复杂度。因此，我们必须为外推位置使用可变长度的样本缓冲区。

## 编程问题

这个模块使用C++语言在Win32环境中利用OpenGL和GLUT图形支持实现。在本节中，我们将介绍我们的虚拟摄像机模型和其他辅助数据结构，它们可以轻松应用于OpenGL。

## OpenGL中的摄像机

首先，让我们看看如何在OpenGL中使用GLUT定义透视视图。我们使用了两个函数来定义视图。第一个是

```
gluPerspective(fov, width/height, nearDist, farDist);
```

fov（视野）是摄像机的垂直视角，以度为单位。使用长焦镜头时该值可以很小，而使用广角镜头时可以很大。如果要模拟缩放，需要不时更改此变量。width/height的值定义了渲染视图的宽高比，应与屏幕相同以避免失真。最后两个参数nearDist和farDist定义了摄像机眼睛到近裁剪平面和远裁剪平面的距离。场景出现在这两个平面之间。

摄像机定义的基本函数如下：

```
gluLookAt(eye.X(), eye.Y(), eye.Z(),
 target.X(), target.Y(), target.Z(),
 up.X(), up.Y(), up.Z());
```

通过此调用，我们可以定义摄像机眼睛的实际位置、目标点以及摄像机的上向量。在计算机游戏中，场景始终在变化。如果摄像机也在变化，我们需要在两个函数中逐帧重新计算这些变量。

## 可变视野，自动缩放

我们的摄像机模型具有自动缩放功能。我们的摄像机可以考虑被跟随对象的大小及其与摄像机的距离，从而在每个时间步长计算fov：

```
fov = 2.0 *
 atan((targetSize / 2.0) / (target - eye).Length()) *
 180.0 / M_PI;
```

你可以注意到，在我们的代码片段中，我们使用了摄像机眼睛与其目标之间的距离，而不是摄像机眼睛与对象本身之间的距离。这样做的理由是，摄像机的目标始终代表被跟随对象的*直接*或*间接*位置。间接情况发生在应用低通滤波和外推后，目标偏离对象的实际位置时。

## 实现人类行为

现在我们将讨论在摄像机模型中实现人类摄像机移动模型。摄像机具有各种数据成员和成员函数。在这里，我们将介绍最重要的几个。

在定义Camera类的camera.h头文件开头，有一些全局常量。其中一个定义了用于摄像机目标外推的数组的最大长度。它被称为MAXEXTRAPOLLENGTH，我们使用的值为1000。这个值应该大于所用计算机中渲染场景的最大帧率，因为使用此长度定义的列表应该存储逐帧收集的一秒钟的向量。

Camera类的其他重要成员是定义摄像机本身（eye、target和up）的Vector3f变量。Vector3f数组（objPosList、objPosDifList、objPosDifDifList和upPosObjList）以及float数组（objFrameWeightList和sumWeight）用于外推。前三个数组是位置、类速度和类加速度样本的集合，而第四个数组保留用于低通滤波位置样本。第一个float数组存储权重，我们在其中定义对应objPosDifList和objPosDifDifList元素的重要性，而第二个列表包含用于平均计算的每个元素编号的预计算权重和。

这些数组按时间顺序存储数据。索引为0的元素对应当前帧，而索引为n的另一个元素表示n帧前的过去。

在这里，你可以看到我们虚拟摄像机模型的人类行为精神。这个函数（称为placeObjectHereToFollow()）获取被跟随对象的实际位置（objPos）和一个标志（lookAtItExactly），以知道目标应该直接跟随它还是带有人类特性地跟随。

```
void placeObjectHereToFollow(Vector3f objPos,
                             bool lookAtItExactly = false) {
    if (actualFPS == 0.0) return;
}
```

该函数以一个控制开始。如果实际帧率为零，这在应用程序刚启动时可能会持续一段时间，我们跳过此执行以避免故障。

然后我们定义那些时间相关的参数，它们从实际帧率（actualFPS）计算得出。浮点变量lengthForExtrpl和lengthForLPF及其整数版本（称为iLengthForExtrpl和iLengthForLPF）包含用于外推或低通滤波的样本数量。换句话说，它们代表外推的时间常数（在我们的示例中为0.7秒）和低通滤波的时间常数（0.4秒，即LPF的2.5 Hz极限频率）。

```
float LengthForExtrpl =
    min(actualFPS, (float)MAXEXTRAPOLLENGTH) * 0.7;
float LengthForLPF =
    min(actualFPS, (float)MAXEXTRAPOLLENGTH) * 0.4;
```

在代码的下一部分，我们使用存储在objPosList中的被跟随对象的一组原始样本来计算下一个低通滤波样本。

```
Vector3f lpfObjectLastPos = objPos;
for (int i = 0; i < (iLengthForLPF - 1); i++)
    lpfObjectLastPos += objPosList[i];
if (iLengthForLPF == 0)
    lpfObjectLastPos *= (1 / (float)iLengthForLPF);
else lpfObjectLastPos = objPos;
```

无论发生什么，我们始终按完整长度逐帧移动前面提到的列表。

```
for (int i = MAXEXTRAPOLLENGTH - 1; i > 0; i--)
{
    objPosList[i] = objPosList[i - 1];
    lpfObjPosList[i] = lpfObjPosList[i - 1];
    objPosDifList[i] = objPosDifList[i - 1];
    objPosDifDifList[i] = objPosDifDifList[i - 1];
}
```

移动后，将新值插入第0位置。请注意，存储类速度数据的列表将LPF样本的差值作为新元素。

```
objPosList[0] = objPos;
lpfObjPosList[0] = lpfObjectLastPos;
objPosDifList[0] = lpfObjPosList[0] - lpfObjPosList[1];
objPosDifDifList[0] = objPosDifList[0] - objPosDifList[1];
```

在这里，我们计算类速度和类加速度数据的加权平均值。

```
Vector3f averageTargetStep;
Vector3f averagePosDif;
for (int i = 0; i < iLengthForExtrpl - 1; i++)
{
    averageTargetStep +=
        (objPosDifList[i] * objFrameWeightList[i]);
    averagePosDif +=
        (objPosDifDifList[i] *
        objFrameWeightList[iLengthForExtrpl - i - 1]);
}
averageTargetStep *= (1 / sumWeight[iLengthForExtrpl - 1]);
averagePosDif *= (1 / sumWeight[iLengthForExtrpl - 1]);
```

如果我们想直接跟随，我们就让函数将目标“附着”到对象上。否则，我们取外推开始时低通滤波位置列表中的元素（即0.7秒前），并用平均速度乘以外推时间和低通滤波时间的一半来增加它。作为最终修正，向其中添加平均加速度。

```
if (lookAtItExactly) { target = objPos; return; }
target = lpfObjPosList[iLengthForExtrpl] +
averageTargetStep *
(LengthForExtrpl + LengthForLPF / 2.0) +
averagePosDif;
}
```

你可能会问，为什么计算中正好使用了LPF时间常数的一半。答案很简单：生成低通滤波位置数据时，我们执行了平均计算。让我们来看一下我们需要用摄像机目标跟随的物体的直线匀速运动。取iLengthForLPF个相邻位置样本并求平均值。这将得到这些样本的算术平均值。在这样的运动中，向量的算术平均值将是由这些样本向量定义的段的中心。按时间顺序，该中心点在时间上也位于该段的中心。如果我们取lpfObjPosList的第一个元素（索引为0），它是在这样的运动期间生成的，它指向一个在半个iLengthForLPF时间之前经过的位置。因此，延迟是（lengthForLPF / 2）。如果我们取该列表中索引为iLengthForExtrpl的元素，总延迟将是（iLengthForExtrpl + lengthForLPF / 2）。这个时间乘以平均速度将在直线匀速运动的情况下得到被跟随对象的实际位置。这就是算法能够在直线段上跟上对象的原因。在其他类型的运动中，跟随的性质将更具人性化。

## 结论

我们描述了一种为驾驶应用程序添加人类摄像机控制的算法。该算法实现简单，模拟了摄像机操作员的惯性以及努力跟上虚拟汽车运动的挣扎。我们算法的性能不依赖于帧率或汽车的速度。该算法的主要优点是它只需要很少的处理时间，因此不会显著降低性能。

