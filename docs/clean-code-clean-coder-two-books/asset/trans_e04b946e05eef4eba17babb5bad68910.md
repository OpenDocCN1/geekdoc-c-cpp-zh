

```java
private void validateSchemaElementId(char elementId) throws
ParseException {
    if (!Character.isLetter(elementId)) {
        throw new ParseException(
            "Bad character:" + elementId + "in Args format: " + schema, 0);
    }
}

private void parseBooleanSchemaElement(char elementId) {
    booleanArgs.put(elementId, false);
}

private void parseIntegerSchemaElement(char elementId) {
    intArgs.put(elementId, 0);
}

private void parseStringSchemaElement(char elementId) {
    stringArgs.put(elementId, "");
}

private boolean isStringSchemaElement(String elementTail) {
    return elementTail.equals("*");
}

private boolean isBooleanSchemaElement(String elementTail) {
    return elementTail.length() == 0;
}

private boolean isIntegerSchemaElement(String elementTail) {
    return elementTail.equals("#");
}

private boolean parseArguments() throws ArgsException {
    for (currentArgument = 0; currentArgument < args.length;
currentArgument++)
    {
```

```java
private boolean isStringArg(char argChar) {
    return stringArgs.containsKey(argChar);
}

private void setBooleanArg(char argChar, boolean value) {
    booleanArgs.put(argChar, value);
}

private boolean isBooleanArg(char argChar) {
    return booleanArgs.containsKey(argChar);
}

public int cardinality() {
    return argsFound.size();
}

public String usage() {
    if (schema.length() > 0)
        return "[-" + schema + "]";
    else
        return "";
}

public String errorMessage() throws Exception {
    switch (errorCode) {
        case OK:
            throw new Exception("TILT: Should not get here.");
        case UNEXPECTED_ARGUMENT:
            return unexpectedArgumentMessage();
        case MISSING_STRING:
            return String.format("Could not find string parameter for -%c.",
                                 errorArgumentId);

        case INVALID_INTEGER:
            return String.format("Argument -%c expects an integer but was
'%s'.",
                                 errorArgumentId,
                                 errorParameter);
        case MISSING_INTEGER:
            return String.format("Could not find integer parameter for -%c.",
                                 errorArgumentId);
    }
    return "";
}

private String unexpectedArgumentMessage() {
    StringBuffer message = new StringBuffer("Argument(s) -");
    for (char c : unexpectedArguments) {
        message.append(c);
    }
    message.append(" unexpected.");

    return message.toString();
}

private boolean falseIfNull(Boolean b) {
    return b != null && b;
}

private int zeroIfNull(Integer i) {
    return i == null ? 0 : i;
}

private String blankIfNull(String s) {
    return s == null ? "" : s;
}

public String getString(char arg) {
    return blankIfNull(stringArgs.get(arg));
}

public int getInt(char arg) {
    return zeroIfNull(intArgs.get(arg));
}
```

```java
private void parseSchemaElement(String element) {
    if (element.length() == 1) {
        parseBooleanSchemaElement(element);
    }
}

private void parseBooleanSchemaElement(String element) {
    char c = element.charAt(0);
    if (Character.isLetter(c)) {
        booleanArgs.put(c, false);
    }
}

private boolean parseArguments() {
    for (String arg : args)
        parseArgument(arg);
    return true;
}

private void parseArgument(String arg) {
    if (arg.startsWith("--"))
        parseElements(arg);
}

private void parseElements(String arg) {
    for (int i = 1; i < arg.length(); i++)
        parseElement(arg.charAt(i));
}

private void parseElement(char argChar) {
    if (isBoolean(argChar)) {
        numberOfArguments++;
        setBooleanArg(argChar, true);
    } else
        unexpectedArguments.add(argChar);
}
```

```java
}
}
```

可以看到，这已经开始失控了。虽然还不算太糟，但混乱肯定在滋生蔓延。这是一堆杂物，但还不至于溃烂。直到加入了整数参数类型，这堆杂物才开始真正发酵、溃烂。

## 于是我停了下来

我至少还要添加两种参数类型，而且我知道它们会让情况变得更糟。如果我硬着头皮一路蛮干下去，或许能让它们工作起来，但会留下一个大到无法收拾的烂摊子。如果这段代码的结构还有希望变得可维护，那么现在就是修复它的时机。

于是我不再添加新功能，而是开始重构。刚刚添加了`String`和整数参数，我就知道每种参数类型都需要在三个主要位置编写新代码。首先，每种参数类型都需要某种方式来解析其模式元素，以便为该类型选择对应的`HashMap`。其次，每种参数类型都需要从命令行字符串中解析出来，并转换为其真实类型。最后，每种参数类型都需要一个`getXXX`方法，以便以其真实类型返回给调用者。

许多不同的类型，却都有相似的方法——这在我看来就是一个类。于是，`ArgumentMarshaler`的概念诞生了。

## 论增量式开发

毁掉一个程序的最佳方式之一，就是以改进的名义对其结构进行大规模修改。有些程序永远无法从这种“改进”中恢复过来。问题在于，要让程序在“改进”之后还能像之前一样正常工作，是非常困难的。

## Args：初稿

为了避免这种情况，我遵循测试驱动开发（TDD）的纪律。这种方法的核心教义之一，就是让系统始终保持运行状态。换句话说，使用TDD时，我不允许做出任何会破坏系统的改动。显然，眼前这个改动不会破坏任何东西。于是，我做了我能想到的最简单的修改，一个尽可能少破坏的修改。我把`Boolean`参数的`HashMap`改为存放`ArgumentMarshaller`。

```java
private Map<Character, ArgumentMarshaller> booleanArgs =
    new HashMap<Character, ArgumentMarshaller>();
```

这个改动破坏了几条语句，我很快修复了它们。

```java
...
private void parseBooleanSchemaElement(char elementId) {
    booleanArgs.put(elementId, new BooleanArgumentMarshaller());
}
```

```java
...
private void setBooleanArg(char argChar, boolean value) {
    booleanArgs.get(argChar).setBoolean(value);
}
```

```java
...
public boolean getBoolean(char arg) {
    return falseIfNull(booleanArgs.get(arg).getBoolean());
}
```

请注意，这些改动恰好发生在我之前提到的几个位置：参数类型的`parse`、`set`和`get`方法。不幸的是，尽管这个改动很小，一些测试还是开始失败了。如果你仔细查看`getBoolean`，就会发现，如果传入'y'调用它，但参数列表中并没有y，那么`booleanArgs.get('y')`将返回`null`，函数就会抛出`NullPointerException`。`falseIfNull`函数原本是用来防止这种情况的，但我所做的改动让该函数变得无关紧要了。

增量式开发要求我在做其他任何改动之前，先快速让这部分恢复正常工作。事实上，修复并不太难。我只需要把对`null`的检查换个位置。我需要检查的不再是`boolean`是否为`null`，而是`ArgumentMarshaller`是否为`null`。

首先，我移除了`getBoolean`函数中对`falseIfNull`的调用。它现在已经没用了，所以我连这个函数本身也一并删除了。测试仍然以同样的方式失败，因此我有信心没有引入任何新的错误。

```java
public boolean getBoolean(char arg) {
    return booleanArgs.get(arg).getBoolean();
}
```

```java
}
```

接下来，我把这个函数拆成两行，将`ArgumentMarshaller`存放到一个名为`argumentMarshaller`的变量中。我不喜欢这个冗长的变量名，它过于冗余，让函数显得杂乱。于是，我把它缩短为`am`[N5]。

```java
public boolean getBoolean(char arg) {
    Args.ArgumentMarshaller am = booleanArgs.get(arg);
    return am.getBoolean();
}
```

然后，我加入了空值检测逻辑。

```java
public boolean getBoolean(char arg) {
    Args.ArgumentMarshaller am = booleanArgs.get(arg);
    return am != null && am.getBoolean();
}
```

## 字符串参数

添加字符串参数与添加布尔参数非常相似。我需要修改`HashMap`，并让parse、set和get函数正常工作。接下来的内容应该不会让你感到意外，唯一可能让你感到意外的或许是，我似乎把所有编组（marshalling）实现都放在了`ArgumentMarshaller`基类中，而不是将其分发给各个派生类。

```java
private Map<Character, ArgumentMarshaller> stringArgs =
    new HashMap<Character, ArgumentMarshaller>();
```

```java
...
private void parseStringSchemaElement(char elementId) {
    stringArgs.put(elementId, new StringArgumentMarshaller());
}
```

```java
...
private void setStringArg(char argChar) throws ArgsException {
    currentArgument++;
    try {
        stringArgs.get(argChar).setString(args[currentArgument]);
    } catch (ArrayIndexOutOfBoundsException e) {
        valid = false;
```

