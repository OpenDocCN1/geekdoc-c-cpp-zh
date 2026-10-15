

```
@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html'
})
export class ProductListComponent {
  onNotify(message: string): void { }
}
```

我们的目标是什么？当用户点击其中一个星级评分时，我们希望在产品列表组件的标题中显示该评分。此功能可能并不非常有用，但它演示了如何将事件从嵌套的子组件传递到父容器组件。我们已向嵌套组件添加了事件绑定。当用户点击星星时，它会记录一条消息。我们反而希望将该字符串消息作为事件发送给容器组件。我们回到示例应用程序，查看 star.component 组件和模板。

![](img/0155736aec718cf18821e9f10a5d308d_163_0.png)

回想一下嵌套组件如何向其容器发送数据，它使用带有 Output 装饰器的事件。让我们定义一个 ratingClicked

Output 装饰器是一个函数，因此我们添加括号。我们再次使用快速修复将 output 添加到 import 语句中。在此示例中，我们仅使用 Output 装饰器装饰嵌套组件的一个属性，但我们并不限于一个。我们可以根据需要公开多个输出属性。

```
import { Component, EventEmitter, Input, OnChanges, Output }

@Component({
  selector: 'pm-star',
  templateUrl: './star.component.html',
  styleUrls: ['./star.component.css']
})
export class StarComponent implements OnChanges {
  @Input() rating: number = 0;
  cropWidth: number = 75;
  @Output() ratingClicked: EventEmitter<string> =
    new EventEmitter<string>();

  ngOnChanges(): void {
    this.cropWidth = this.rating * 75/5;
  }

  onClick(): void {
    console.log(`The rating ${this.rating} was clicked!`);
  }
}
```

在我们的 star 组件的 onClick 方法中，我们不想再记录此消息，而是希望发出我们的 ratingClicked 事件并将消息传递给容器组件。我们使用事件属性并调用其 emit 方法，将期望的字符串传入。

```
onClick(): void {
  this.ratingClicked.emit(`The rating ${this.rating} was clicked!`);
}
```

现在我们已向容器发出此 ratingClicked 事件，容器如何监听并响应该事件？它使用事件绑定。在模板中，我们使用事件绑定将 StarComponent 发出的事件绑定起来。对于事件绑定，我们使用括号并指定要监听的事件名称。我们要监听 StarComponent 的 ratingClicked 事件。

事件发生时，我们调用一个方法。让我们称之为 onRatingClicked。回想一下我们在引发此事件时传递了一个字符串，因此让我们将该字符串传递给我们的 onRatingClicked 方法。我们使用 $event 来做到这一点，$event 会传递与生成的事件关联的任何数据。

```
<> product-list.component.html ×
45   <td>{{product.productName}}</td>
46   <td>{{ product.productCode | lowercase | convert
47   <td>{{ product.releaseDate }}</td>
48   <td>{{ product.price | currency:'USD':'symbol':''
49   <td>
50     <pm-star [rating]='product.starRating'
      (ratingClicked)='onRatingClicked($event)'>
     </pm-star>
   </td>
   </tr>
```

接下来，我们需要在类中编写此方法代码。我们的模板期望我们有一个名为 onRatingClicked 的方法，并且会将事件的字符串消息传递给它。我们的方法不返回值，因此我们将返回类型定义为 void。现在我们已从事件中获取了消息，我们想用它做什么？我们的目标是在页面标题上显示它，因此我们将修改 pageTitle 以显示 Product List 和来自嵌套 StarComponent 的消息。

```
toggleImage(): void {
  this.showImage = !this.showImage;
}

ngOnInit(): void {
  this.listFilter = 'cart';
}

onRatingClicked(message: string): void {
  this.pageTitle = "Product List: " + message;
}
```

这并不是一个非常现实的示例，但我想尽可能保持简单。让我们用一些清单来收尾，我们可以在构建可嵌套组件时使用。我们刚刚看到容器如何通过绑定到用 @Input 装饰器装饰的嵌套组件属性来向嵌套组件传递数据，以及嵌套组件如何使用用 @Output 装饰器装饰的事件属性来引发事件。我们可以将用 @Input 或 @Output 装饰器装饰的属性视为可嵌套组件的公共 API。

```
export class StarComponent {
  @Input() rating: number;
}
```

组件中的其他所有内容都被封装起来，只能由组件的模板和类访问。只要嵌套组件属性需要从其容器获取输入数据，就用 @Input 装饰器装饰它。任何类型的组件属性都可以用 @Input 装饰器装饰。不要忘记 @ 前缀，并且由于 @Input 装饰器是一个函数，请在其后加上打开和关闭的括号。只要嵌套组件属性需要发出事件并可选地将数据传递给其容器，就用 @Output 装饰器装饰它。仅应将类型为 EventEmitter 的属性标记为 @Output。 使用 EventEmitter 的泛型参数指定事件数据的类型，并使用 new 关键字创建新的事件。

```
export class StarComponent {
  @Output() notify: EventEmitter<string> =
      new EventEmitter<string>();
}
```

不要忘记 @ 前缀，并且由于 @Output 装饰器是一个函数，请在其后加上打开和关闭的括号。在容器组件的模板中，将嵌套组件用作指令。

```
<pm-star [rating]='product.starRating'
    (notify)='onNotify($event)'>
</pm-star>
```

对于指令的名称，使用嵌套组件的选择器。使用属性绑定将数据传递给嵌套组件。使用事件绑定响应来自嵌套组件的事件，并使用 $event 访问从嵌套组件传递的事件数据。总结一下，我们构建了 Star 组件并将其嵌套在 Product List 组件中。我们可以在应用程序的任何其他组件中重用此组件，例如 Product Detail 组件。接下来，让我们看看如何构建 Angular 服务，这样我们就不需要在组件中存放产品数据了。

## 第 19 章 如何构建服务

组件很好，但对于与特定视图无关或我们希望在组件之间共享的数据或逻辑，我们该怎么办？我们构建服务。在本章中，我们创建一个服务并使用依赖注入将该服务注入到任何需要它的组件中。应用程序通常需要诸如产品数据服务或日志服务之类的服务。我们的组件依赖这些服务来完成繁重的工作。如果 Angular 能把这些服务端上来就好了？嗯，是的，它可以，但服务到底是什么？服务是一个具有专注目的的类。我们经常创建服务来实现独立于任何特定组件的功能、在组件之间共享数据或逻辑，或封装外部交互，例如数据访问。通过将这些职责从组件转移到服务，代码更易于测试、调试和重用。在本章中，我们首先概述 Angular 中服务和依赖注入的工作原理。然后我们将构建一个服务，注册该服务，并检查如何在组件中使用该服务。我们目前已在应用程序中实现了几个部分，但我们的数据直接在产品列表组件中。我们将把提供产品数据的责任转移到产品数据服务。在我们开始构建服务之前，让我们先看看 Angular 中服务和依赖注入的工作原理。我们的组件有两种方式可以与此服务配合工作。组件可以创建服务类的实例并使用它。这很简单，而且有效。但实例是

