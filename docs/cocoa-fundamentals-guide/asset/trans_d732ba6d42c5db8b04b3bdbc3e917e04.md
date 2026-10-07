

## 第3 章
为 Cocoa 程序添加行为

对于布尔属性，采用变体形式的 getter 方法是可以接受的。在这种情况下，它的形式为 `isAttribute`。例如，一个名为 `hidden` 的布尔类型实例变量将有一个 `isHidden` getter 方法和一个 `setHidden` setter 方法。

如果实例变量是标量类型（如 `int` 或 `float`），则访问器方法的实现通常非常简单。类型为 `float` 的实例变量 `currentRate` 在列表 3-5 显示了如何实现访问器方法。

### 列表 3-5 为标量实例变量实现访问器

```
(float)currentRate {
    return currentRate;
}
```

```
(void)setCurrentRate:(float)newRate {
    currentRate = newRate;
}
```

如果启用了垃圾回收，对于对象值属性的 setter 访问方法的实现也只是简单的赋值。列表 3-6 显示了你如何实现此类方法。

### 列表 3-6 为对象实例变量实现访问器（启用垃圾回收）

```
(NSString*)jobTitle {
    return jobTitle;
}
```

```
(void)setJobTitle:(NSString*)newTitle {
    jobTitle = newTitle;
}
```

当实例变量持有对象且未启用垃圾回收时，情况就会变得微妙。因为这些对象必须是持久的，并且在赋值时必须被创建、复制或保留。当 setter 访问器更改实例变量的值时，它只负责确保持久性，而不负责妥善处理旧值。getter 则将实例变量的值传递给请求的对象。鉴于 Cocoa 对象所有权策略的两个假设，这两种类型的访问器操作对内存管理都有影响：

- 从方法返回的对象（例如通过 getter 访问返回）在调用对象的作用范围内是有效的。换句话说，保证该对象在该作用范围内不会被释放或更改值。
- 当调用对象从方法作为访问器接收到一个对象时，除非它显式地保留（retain）或复制（copy）了该对象，否则不应释放该对象。

考虑到这两个假设，让我们看看名为 `title` 的 `NSString` 实例变量的 getter 和 setter 访问器的两种可能实现。列表 3-7 显示了第一种。

### 列表 3-7 为对象实例变量实现访问器——良好的技术

```
(NSString*)jobTitle {
    return jobTitle;
}
```

```
(void)setTitle:(NSString*)newTitle {
if (title != newTitle) {
    title autorelease;
    title = [newTitle copy];
}
}
```

注意，getter 访问器只是返回实例变量。相反，setter 访问器则很忙。在验证传入的实例变量值与当前值不同后，在复制新值之前对当前值进行自动释放。（向对象发送 `autorelease` 比发送 `release` 更“线程安全”）。然而，这种方法仍然存在潜在的危险。如果客户端正在使用 getter 返回的对象，而此时 setter 访问器自动释放了 `NSString` 对象，并在不久后该对象被释放并销毁，那么客户端对实例变量的引用将不再有效。

列表 3-8 显示了访问器方法的实现，该方法通过在 getter 中保留（retain）和自动释放（autorelease）实例变量来绕过这个问题。

### 列表 3-8 为对象变量实现访问器——更好的技术

```
(NSString *)title {
    return [[self retain] autorelease];
}
(void)setTitle:(NSString *)newTitle {
    if (title != newTitle) {
        [title autorelease];
        title = [newTitle copy];
    }
}
```

在上述两个 setter 方法示例（列表 3-5 和列表 3-7）中，新的 `NSString` 变量是被复制的而不是保留的。通用规则是：如果没有被保留，你就应该复制它。如果一个实例是一个值对象——即代表字符串、日期、数字或记录等内容的对象——你应该复制它。换句话说，你想要该对象的自己的副本。

然而，如果要存储和访问的对象是一个对象实体（例如 `UIView` 或 `NSWindow`），你应该保留它。实体的开销更高且具有关联性，复制它们可能是昂贵的。判断一个对象是值对象还是实体的一种方法，是决定你感兴趣的是对象的值还是对象本身。如果你感兴趣的是值，它就是一个值对象，你应该复制它（当然，假设该对象符合 `NSCopy` 协议）。

在 setter 中决定保留还是复制实例变量的另一种方法，是确定实例是属性（attribute）还是关系（relationship）。这对于模型对象特别有用，模型对象是代表应用程序数据的对象。属性本质上与值对象相同：它是封装该对象的定义特征，例如颜色（`NSColor`）或标题。另一方面，关系仅仅是如此：保留与一个或多个对象的关系（通过引用）。通常情况下，在 setter 方法中，你复制属性的值并保留关系。然而，关系具有基数（cardinality）；它们可以是一对一或一对多的。一对多关系（通常由集合对象，如 `NSArray` 实例表示表示）可能需要 setter 方法执行一些比简单保留实例变量之外的操作。详情请参阅《模型对象实现指南》。关于作为属性或关系的对象属性，请参阅“键值机制”（第 128 页）。

