
数据的退出。

### Serial.find(string)

这将在 Serial 提供的数据中搜索给定字符串。如果找到该字符串，方法将返回 true。如果未找到该字符串，方法将返回 false。

### Serial.findUntil(string, 可选 endString)

这将在串口缓冲区中查找该字符串，直到找到该字符串或找到指定的终止字符串。如果找到目标字符串，则方法将返回 true。如果找到终止字符串或方法超时，则返回 false。

### Serial.flush()

这将允许你暂停进程，直到发送到串口的所有数据都已发送完毕。很简单！

### Serial.parseFloat()

这将返回串口流提供的第一个浮点数。它会在遇到任何非浮点字符时结束。

### Serial.parseInt()

这将返回串口流提供的第一个整数。它会在遇到第一个非数字字符时结束。

### Serial.peek()

这将返回串口缓冲区接下来要导入的字符。但是，它不会从缓冲区中移除该字符。这使它与我们稍后将介绍的 Serial.read() 方法有本质区别。这意味着你可以直接查看下一个字符是什么。

### Serial.print(value, 可选 format)

你可以选择指定格式。否则，整数默认按十进制打印；浮点数默认打印到两位小数，依此类推。

你可以将字符或字符串原样发送给 print 语句，它会顺利打印它们。

### Serial.println(value, 可选 format)

这将允许你像使用普通 print 方法一样打印值。

### Serial.read()

这将读取通过串口传入的数据。很简单！它会被添加到称为串口缓冲区的传入串口数据流中。当你从这个缓冲区读取时，信息会被销毁，因此如果你以后需要重用数据，请务必将其保存到变量中。

### Serial.readBytes(serialBuffer, numberOfBytes)

这将从串口读取字符到缓冲区。你可以确定要读取的字节数。缓冲区必须是 char 数组或 byte 数组。

### Serial.readBytesUntil(terminatorCharacter, serialBuffer, numberOfBytes)

这将从串口读取字符，直到读取了给定数量的字节，或读取到给定的终止字符。无论哪种情况，方法都会终止。

### Serial.write()

这将向串口写入数据；但是，这个特定方法只向串口发送二进制数据。如果你需要发送 ASCII 数据，则应改用 print 方法。

### Serial.serialEvent()

每当串口有数据可供使用时，就会调用此函数。然后你可以使用 Serial.read() 函数从串口读取数据。

至此，我们已经介绍了与 Serial 类相关的许多特定函数，以及它与 Arduino API 编程的关系。接下来我们需要处理的是 Ethernet 类。

## 用户自定义函数

保持代码整洁、有条理且模块化（可重用）的方法之一，就是在代码中使用函数。此外，函数通过让某些部分可重用来帮助缩小代码体积。顾名思义，函数就像为服务特定功能而创建的工具。

虽然我们已经遇到过一些用户自定义函数，但现在将更详细地介绍它们，并解释上次遇到时可能略过的一些特性。现在让我们看看函数的声明：

```cpp
float employeeEarnings(float hoursWorked, float payRate) {
  float result; // this will be the value we return when this function is called. It should match the datatype before our function name.
  result = hoursWorked * payRate;
  return result; // return tells the function to send a value back once to where it was called
}
```

这个函数显然接受两个参数：hoursWorked 和 payRate，二者都是“float”类型。它对它们进行一些简单的数学运算，然后返回一个 float 值。return 意味着终止函数，并将在 return 一词之后放置的任何值（通常是变量）作为某些计算的结果发送回去。

现在让我们调用这个函数来获取员工的收入：

```cpp
void loop () {
  float hoursWorked = 37.5;
  float payRate = 18.50;
  float result = employeeEarnings(hoursWorked, payRate);
  // result will be 693.75
```

首先，函数必须在任何其他函数之外声明。这意味着你需要在 setup() 或 loop() 或任何其他用户自定义函数之外编写正在创建的函数代码。

让我们看另一个示例——一个可用于平滑传感器读数的示例 sketch：

```cpp
int sensorSmoothing(int analogPin) {
  int sensorValue = 0;

  for (int index = 0; index < 5; index++) {
    digitalWrite(LED_BUILTIN, HIGH); // Turn on LED for smoothing
    sensorValue = sensorValue + analogRead(analogPin);
    delay(100); // 100 millisecond delay between samples
  }

  digitalWrite(LED_BUILTIN, LOW); // turn off LED
  sensorValue = sensorValue / 5; // average the values over five samples
  return sensorValue;
}
```

如果许多传感器容易出现抖动输入，这种函数可用于平滑它们的数据输入。这将对采样值求平均，以提供更一致的数据流。你可以看到，这段代码与我们上一个示例非常相似：

```cpp
void loop () {
  int sensorPin = 0; // analog pin 0
  int sensorValue = sensorSmoothing(sensorPin);
}
```

在这里，当我们尝试初始化 sensorValue 变量时，它会在模拟引脚 0 上调用 sensorSmoothing() 函数，并返回五次采样的平均结果。

函数也不总是需要参数或返回变量。有时函数可以不返回值，也没有参数。它们所做的只是执行几行代码，然后终止，让编译器返回到调用它们的代码位置。

## 结论

下一步就是走出去，开始制作你自己的 sketch！去当地的爱好商店找些灵感，或者去社区看看你可能想尝试哪些新项目。在你对下一步想做什么有了想法之后，（机器人非常有趣！）加入社区吧！说真的，和朋友一起构建项目并互相比较会非常有趣。如果你觉得自己不知道从哪里开始，别担心！有许多在线资源分享编码和技巧来提升你的水平。许多在线网站还设有论坛，专门帮助像你这样的人学习并展示自己的成果。这也是作为爱好者学习和成长的绝佳方式。

如果你想开始但感觉手头拮据，也有选择。正如我们上面所说，Arduino 网站和其他地方有相当便宜的模块可供购买。此外，还有更便宜的编程语言可用，有些甚至免费。学习这些语言实际上比你想象的更容易。如果你懂一种编程语言，其余的会更容易理解和编写。当地图书馆也有书可以帮助你学习如何编码。许多图书馆提供馆际互借，这意味着你可以通过来自周围各地的书籍学习编程！最棒的是，从图书馆借书学习完全免费！如果你对此有任何疑问，请记住，你可以上网找到其他使用过 Arduino 并知道如何帮助你入门的人。

Arduino 板可以编程来控制 LED 点亮或渐变等。Arduino 编程中使用的语法与 C++ 类似。如果你擅长 C++，那么用 Arduino 编程对你来说会很容易。Arduino 中的变量在 setup() 函数中初始化。loop() 部分包含要重复运行的代码块。使用 Arduino 引脚时，你必须指定需要使用的引脚。引脚通常用数字标识，因为每个引脚都有唯一编号。拿到板子后，你必须在计算机上设置 Arduino IDE。这是你在将 Arduino 代码上传到板子之前编写代码的地方。Arduino 代码通常称为 sketch。你必须获得电源。但是，某些板型必须经过配置，才能允许从计算机获取电力。sketch 对板子的效果将在上传到板子后显现，此时需要点击 Upload 按钮。

每个 Arduino 都有许多传感器和扩展件，所以请务必检查
