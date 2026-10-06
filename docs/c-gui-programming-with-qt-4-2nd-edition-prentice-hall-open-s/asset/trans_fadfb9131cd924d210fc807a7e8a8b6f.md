

```cpp
if (event->timerId == myTimerId) {
    ++offset;
    if (offset >= fontMetrics().width(text)) {
        offset = 0;
        scroll(-1, 0);
    }
} else {
    QWidget::timerEvent(event);
}
```

系统会间隔调用 `timerEvent()` 函数。它将 `offset` 增加 1 以模拟移动，并在文本宽度处回绕。然后，它使用 `QWidget::scroll()` 将部件的内容向左滚动一个像素。调用 `update()` 代替 `scroll()` 就足够了，但 `scroll()` 更高效，因为它只是移动屏幕上现有的像素，并且仅为部件新显示的区域（在本例中为1像素宽的条带）生成绘制事件。

如果定时事件不是我们感兴趣的定时器，我们将其传递给基类。

```cpp
void Ticker::hideEvent(QHideEvent / /* event */)
{
    killTimer(myTimerId);
    myTimerId = 0;
}
```

`hideEvent()` 函数调用 `QObject::killTimer()` 来停止定时器。
定时器是低层的，如果我们需要多个定时器，跟踪所有的定时器 ID 会变得繁琐。在这种情况下，通常为每个定时器创建一个 `QTimer` 对象更简单。`QTimer` 在每个时间间隔都会发射 `timeout()` 信号。`QTimer` 还为单次定时器（仅超时一次的定时器）提供了一个方便的接口，正如我们在第6章（第158页）中所看到的。

## 安装事件过滤器

Qt 事件模型的一个非常强大的特性是，可以设置一个 `QObject` 实例在另一个 `QObject` 实例看到事件之前对其进行监控。

假设我们有一个由多个 `QEdit` 组成的 `CustomerInputDialog` 部件，我们想使用空格键将焦点移动到下一个 `QEdit`。这种非标准行为对于用户接受过相关训练的内部应用程序可能是合适的。一个直接的是子类 `QEdit` 并重新实现 `keyPressEvent()` 来调用 `focusNextChild()`，如下：

```cpp
void MyLineEdit::keyPressEvent(QKeyEvent *event)
{
    if (event->key() == Qt::Key_Space) {
        focusNextChild();
    } else {
        QLineEdit::keyPressEvent(event);
    }
}
```

这种方法有一个主要缺点：如果在表单中使用几种不同类型的部件（例如 `ComboBox` 和 `SpinBoxes`），我们必须对它们进行子类化以产生相同的行为。更好的解决方案是让 `CustomerInputDialog` 监控其子部件的按键事件，并在监控代码中实现所需的行为。可以通过事件过滤器来实现。设置事件过滤器涉及两个步骤：

-   通过在目标对象上调用 `installEventFilter()` 为目标对象注册监控对象。

-   在监控对象的 `eventFilter()` 函数中处理目标对象的事件。

在构造函数中注册监控是一个很好的位置：

```cpp
CustomerInputDialog::CustomerInputDialog(QWidget *parent)
    : QDialog(parent)
{
    ...
    firstNameEdit->installEventFilter(this);
    lastNameEdit->installEventFilter(this);
    cityEdit->installEventFilter(this);
    phoneNumberEdit->installEventFilter(this);
}
```

一旦注册了第一个过滤器，发送到 `firstNameEdit`、`lastNameEdit`、`phoneNumberEdit` 部件的事件在发送到目标位置之前，会首先发送到 `CustomerInfoDialog::eventFilter()` 函数。

这里是接收事件的 `eventFilter()` 函数：

```cpp
bool CustomerInfoDialog::eventFilter(QObject target, QEvent event) {
    if (target == firstNameEdit || target == lastNameEdit
        || target == cityEdit || target == phoneNumberEdit) {
        if (event->type() == QEvent::KeyPress) {
            QKeyEvent *key = static_cast<QKeyEvent>(event);
            if (key->key() == Qt::Key_Space) {
                focusNextChild();
                return true;
            }
        }
    }
    return QDialog::eventFilter(target, event);
}
```

首先，我们检查目标部件是否为 `QLineEdit` 之一。如果事件是按键，我们将其强制转换为 `QKeyEvent` 并检查按了哪个键。

如果按下的键是空格，我们调用 `focusNextChild()` 将焦点传递给焦点链中的下一个部件，并返回 `true` 告诉 Qt 我们已经处理了该事件。如果我们返回 `false`，Qt 将把事件发送到其预期目标，导致 `QLineEdit` 中插入一个多余的空格。

如果目标部件不是 `QLineEdit` 或事件不是空格按键按下，我们将控制权传递给 `eventFilter()` 的基类实现。目标部件也可能是基类 `QDialog` 正在监控的部件。（在 Qt 4.3 中，`QDialog` 并非如此。然而，其他部件类（如 `QScrollArea`）由于各种原因会监控其某些子部件。）

Qt 提供了可以处理和过滤事件的五个级别：

## 1. 我们可以重新实现特定的事件处理器。

重新实现如 `mousePressEvent()` 和 `paintEvent()` 等处理器是处理事件最常用的方法。我们已经见过许多此类例子。

## 2. 我们可以重新实现 `QObject::event()`。

通过重新实现 `event()`，我们可以在事件到达处理器之前拦截它们。这对于没有特定处理器的事件或自定义事件非常有用。

## 3. 我们可以使用事件过滤器。

如所述，事件过滤器是在不对部件进行子类的情况下拦截事件的强大方法。

## 4. 我们可以使用 `QTimer`。

`QTimer` 提供了一种处理基于时间的事件的方便方法。

## 5. 我们可以子类化并重新实现虚方法。

通过对类进行子类化，你可以覆盖它的默认行为并提供虚方法的自己的实现。

