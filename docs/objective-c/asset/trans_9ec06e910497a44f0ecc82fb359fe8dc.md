

## 清单6.3
（续）

```
else if([[column name] isEqualToString:@"lastName"])
    [column setValue:[self lastName]];
else if([[column name] isEqualToString:@"age"])
    [column setValue:[self lastName]];
else if([[column name] isEqualToString:@"birthDate"])
    [column setValue:[self lastName]];
...
}
[row save];
}
```

这段代码很快就会变得相当难处理。现在看看使用键值编码方法的相同代码。清单6.4展示了更新后的代码。

## 清单6.4
### 使用KVC的序列化方法

```
-(BOOL)serializeToTable:(Table *)inTable
{
    Row *row = [inTable addRow];
    for(Column *column in row)
    {
        [column setValue:[self valueForKey:[column name]]];
    }
    [row save];
}
```

如你所见，新版本不仅在代码行数上更少，而且更健壮、更灵活。当你向表中添加新列时，只需额外向这个对象添加属性来存储这些字段的值即可。这个序列化方法会自动从这些属性中提取值并为我们存储，无需对该方法做任何修改。同样，序列化方法并不是你会在代码中到处使用的东西。我想强调这一点。使用KVC访问器而不是普通访问器，通常会产生比你需要的更多的代码。但在这种情况下，它使你能编写更动态的代码，也能减少代码中必须表示对象属性信息的位置数量。当你能够查询一个对象的属性时，就不必把那些信息写入代码中的那么多位置。这总是一件好事——没有写出来的代码才是最没有bug的代码。

## 使用键路径

要使用键值编码，你首先必须弄清楚可以构建哪些键路径，以及通过这些键路径可以访问什么。

你可以把使用KVC访问器想象成使用字典。字典的键是字符串。这些字符串本身就是你正在操作的对象的属性名称。由于这个要求，在键以及属性命名方面必须遵循若干规则。首先，你的键必须使用ASCII编码。这意味着你的键不能使用那些通常不能在属性名中使用的特殊字符。其次，你的键必须以小写字母开头。首字母也允许使用下划线，但不能使用数字，也不能使用大写字母。最后，键中不能包含任何空白字符。

谢天谢地，因为你访问的属性本来就必须是有效的符号名，所以这些规则中的大部分你可能已经在遵守了。

清单6.5展示了一些有效键路径和无效键路径的示例。

## 清单6.5
### 有效与无效的键路径

```
// valid
[foo valueForKeyPath:@"someMember"];
[foo valueForKeyPath:@"someMember.someAttributeOnMember"];
[foo valueForKeyPath:@"someOtherMember"];

// invalid
[foo valueForKeyPath:@"4fun"];
[foo valueForKeyPath:@"kermit the frog"];
[foo valueForKeyPath:@"SomethingWickedThisWayComes"];
[foo valueForKeyPath:@"THISWONTWORK"];
[foo valueForKeyPath:@"thisAlsoWon'tWork"];
```

正如我之前讨论过的，你可以使用键路径遍历对象之间的关系并访问子对象上的属性。键路径是使用点号跨越不同对象之间关系的键，如上面的示例`@"someMember.someAttributeOnMember"`。该键路径访问`foo`对象上的`someMember`属性，找到`someMember`所属类上的`someAttributeOnMember`属性，并返回存储在那里的值。在这些键路径的规范中提供了许多语法糖。除了能够遍历这些关系之外，你甚至可以访问操作对象集合的函数，例如它们的`count`等。例如，清单6.6展示了一些你可以作为这些键路径一部分使用的内置函数。

## 清单6.6
### 在键路径中使用函数

```
[anArrayOfProducts valueForKeyPath:@"@avg.price"];
[anArrayOfProducts valueForKeyPath:@"@sum.cost"];
[store valueForKeyPath:@"products.@count"];
```

这些函数仅适用于对象数组和对象集合。在示例中，前两行访问的是`product`对象。这些产品具有价格和成本等属性。给定的函数获取数组中每个对象指定属性的值，然后对这些值执行指定的函数。换句话说，第一项遍历产品数组中的每一项，收集每个产品的价格，然后计算它们的平均值。

使用这些函数的语法包括：在函数名前加上`@`符号，然后是函数名、一个`.`,再然后是要操作的属性。对操作属性的要求的唯一例外是`@count`函数，它只返回集合中项目的数量。

表6.1列出了这些函数。

| 函数 | 用途 |
|---|---|
| @avg | 返回数组或集合中所有元素的平均值。 |
| @count | 返回数组或集合中元素的数量。 |
| @max | 返回数组或集合中所有元素的最大值。 |
| @min | 返回数组或集合中所有元素的最小值。 |
| @sum | 返回数组或集合中所有元素值的总和。 |
| @unionOfArrays/@distinctUnionOfArrays | 给定一个数组集合，返回一个包含该集合中所有数组的数组。对于distinct版本，它只返回不重复的数组。 |
| @unionOfSets/@distinctUnionOfSets | 给定一个集合的集合，返回一个包含所有这些集合的集合。对于distinct版本，它只返回不重复的集合。 |
| @unionOfObjects/@distinctUnionOfObjects | 给定一个集合或数组的集合，以单个数组的形式返回所有集合中的所有元素。distinct版本只返回不重复的元素。 |

## 编写符合KVC的访问器

Objective-C运行时实现所有这些魔法，部分依赖于底层框架的能力，部分归功于编码风格约定。尽管Objective-C运行时在KVC功能方面承担了繁重的工作，但它依赖于你——开发者——为你的属性编写遵循特定约定的访问器，以便它能通过KVC检索和设置值。

KVC对设置器和获取器的标准是：设置器遵循`set<Value>:`的模式，获取器则遵循简单的`<value>`模式。在这两种情况下，模式中的`<value>`部分都应替换为你正在访问的属性名。该属性应该是一个成员变量，其名称使用驼峰命名法指定。

> 注意
> 术语“驼峰命名法”（camel case）指的是一种变量命名标准，其中变量中的各个单词被合并成一个长字符串。在这个字符串中，除了第一个单词外，每个单词的首字母都大写。例如，要编写一个名为“some variable name”的变量名，你应该写成`someVariableName`。观察这个变量名，你会发现变量名内部的大写字母就像骆驼的驼峰。这就是其名称的由来。

因此，给出一个如清单6.7所示的类定义，你可以写出如清单6.7所示的访问器。

## 清单6.7
### 包含成员变量的类定义

```
@interface MyClass : NSObject
{
    float x;
    float y;
    NSString *something;
}
```

## 清单6.7（续）

```
}
-(void)setX:(float)inX;
-(void)setY:(float)inY;
-(void)setSomething:(NSString *)inSomething;
-(float)x;
-(float)y;
-(NSString *)something;
@end
```

符合KVC的访问器。

```
@implementation MyClass
-(void)setX:(float)inX;
{
    x = inX;
}

-(void)setY:(float)inY;
{
    y = inY;
}

-(void)setSomething:(NSString *)inSomething;
{
    NSString *oldValue = something;
    something = [inSomething retain];
    [oldValue release];
}

-(float)x;
{
    return x;
}

-(float)y;
{
    return y;
}

-(NSString *)something;
{
    return something;
}

@end
```

