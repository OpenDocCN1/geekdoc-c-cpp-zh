

在表格数据元素中，我们希望用我们的 StarComponent 替换 starRating 数字的显示方式。为此，我们只需用我们的指令替换绑定。现在我们的 ProductList 模板将显示我们的星星。接下来我们需要告诉 Angular 在哪里可以找到这个指令。由于我们只有一个 Angular 模块，我们将在其中添加嵌套组件的声明。将 StarComponent 添加到传递给 @NgModule 装饰器的 declarations 数组中。

![](img/0155736aec718cf18821e9f10a5d308d_154_0.png)

这些是我们本书记载在前面使用组件作为指令时所遵循的相同步骤。到目前为止没有什么新东西。我们在 OnChanges 生命周期事件发生时在 ngOnChanges 方法中设置 cropWidth 属性。但 OnChanges 生命周期事件从未发生，因为 OnChanges 只会监视输入属性的变化。我们没有任何输入属性，所以我们有两个问题。我们的 OnChanges 事件不会触发，而且我们目前没有办法从容器中获取正确的评分。

```typescript
export class StarComponent implements OnChanges {
  rating: number = 4;
  cropWidth: number = 75;

  ngOnChanges(): void {
    this.cropWidth = this.rating * 75/5;
  }
}
```

让我们看看输入属性如何能解决这两个问题。在构建交互式应用程序时，嵌套组件通常需要与其容器通信。嵌套组件使用输入属性从其容器接收信息。为了使 StarComponent 显示正确数量的星星，容器必须将产品的评分作为输入传递给我们的 StarComponent。嵌套组件通过发出事件将信息输出回其容器。在我们的示例中，如果用户点击星星，我们希望发出一个事件来通知容器。让我们先关注输入属性。如果嵌套组件想要从其容器接收输入，它必须使用恰如其名的 @Input 装饰器为此目的标识一个属性。我们使用 @Input 装饰器来装饰嵌套组件类中的任何属性。这适用于任何属性类型，包括对象。在本例中，我们希望将 rating 传递给嵌套组件，因此我们用 @Input 装饰器标记该属性。

```typescript
@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html'
})
export class StarComponent {
  @Input() rating: number;
  cropWidth: number;
}
```

容器模板然后使用属性绑定将数据传递给嵌套组件。还记得如何使用属性绑定吗？我们用方括号括起嵌套组件的属性，并将其分配给用引号括起来的表达式。

```html
<td>
  <pm-star [rating]='product.starRating'>
  </pm-star>
</td>
```

在本例中，模板使用属性绑定将产品的 starRating 传递给 StarComponent。容器组件只能绑定到用 @Input 装饰器标记的嵌套组件属性。因此在本例中，模板绑定到 rating 但未绑定到 cropWidth。让我们试试看。以下是 StarComponent 和模板。StarComponent 希望其容器传入 rating。正如我们所见，我们将 @Input 装饰器添加到我们想要传入的任何属性上。它是一个装饰器，所以我们指定 @ 符号。@Input 装饰器是一个函数，所以我们添加括号并添加相关的导入。我们不需要向此函数传递任何内容，所以就这样。

```typescript
import { Component, Input, OnChanges } from "@angular/core";

@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html',
  styleUrls: ['./star.component.css']
})
export class StarComponent implements OnChanges {
  @Input() rating: number = 4;
  cropWidth: number = 75;

  ngOnChanges(): void {
    this.cropWidth = this.rating * 75/5;
  }
}
```

然后我们将默认值重置为 0。

![](img/0155736aec718cf18821e9f10a5d308d_159_0.png)

我们通过在括号内指定事件来定义事件绑定。我们将其绑定到组件中的一个方法，我们称之为 onClick。接下来，我们在组件中编写 onClick 方法。该方法没有返回类型，因此我们指定 void。现在，让我们在每次用户点击星星时向控制台记录一条消息。在这里，我使用 ES2015 反引号来指定 JavaScript 模板字面量。模板字面量允许我们使用占位符在字符串中插入表达式。在此表达式中，我们显示产品评分。

![](img/0155736aec718cf18821e9f10a5d308d_159_1.png)

打开浏览器并打开开发者工具。然后让我们清除默认的 Filter by，以便我们拥有更多产品。点击一个产品，我们会看到星级评分记录到控制台。点击另一个产品，我们会看到其星级评分。

![](img/0155736aec718cf18821e9f10a5d308d_160_0.png)

我们的嵌套组件现在可以在用户点击评分时做出反应，但如果我们想将该事件传递给容器组件怎么办？

我们看到容器如何通过绑定到用 Input 装饰器装饰的嵌套组件属性来向嵌套组件传递数据。如果嵌套组件想要将数据发送回其容器，它可以发出一个事件。嵌套组件必须使用恰如其名的 Output 装饰器为此目的标识一个属性。我们可以使用 Output 装饰器来装饰嵌套组件类的任何属性，然而，该属性必须是事件。嵌套组件将数据传回其容器的唯一方式是通过发出事件。在 Angular 中，事件是使用 EventEmitter 对象定义的。所以在这里，我们创建一个 EventEmitter 的新实例。注意这里的语法。TypeScript 支持泛型。如果您不熟悉泛型，此语法允许我们标识对象将使用的特定类型。

```typescript
@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html'
})
export class StarComponent {
  @Input() rating: number;
  cropWidth: number;
  @Output() notify: EventEmitter<string> =
    new EventEmitter<string>();
}
```

创建 EventEmitter 时，泛型参数标识随事件传递的数据类型。如果我们想在事件中向容器传递一个字符串值，我们在这里定义 string。如果我们想传递多个值，我们可以在这里指定一个对象。在本例中，我们定义了一个带有字符串数据的 notify 事件。当用户点击星星时，只有 StarComponent 接收到该点击事件。

```typescript
@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html'
})
export class StarComponent {
  @Input() rating: number;
  cropWidth: number;
  @Output() notify: EventEmitter<string> =
    new EventEmitter<string>();

  onClick() {

  }
}
```

与其自行处理点击事件，StarComponent 可以向其容器发出新事件并选择性地传递一些数据。

```typescript
@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html'
})
export class StarComponent {
  @Input() rating: number;
  cropWidth: number;
  @Output() notify: EventEmitter<string> =
    new EventEmitter<string>();

  onClick() {
    this.notify.emit('clicked!');
  }
}
```

在本例中，onClick 方法发出 notify 事件并传递一个字符串消息。在容器组件的模板中，我们使用事件绑定绑定到 StarComponent 的 notify 事件，然后在该事件发生时调用容器组件中的一个方法。

```html
<td>
  <pm-star [rating]='product.starRating'
           (notify)='onNotify($event)'>
  </pm-star>
</td>
```

我们使用 $event 访问事件数据。由于事件数据是一个字符串，此方法接收一个字符串。

