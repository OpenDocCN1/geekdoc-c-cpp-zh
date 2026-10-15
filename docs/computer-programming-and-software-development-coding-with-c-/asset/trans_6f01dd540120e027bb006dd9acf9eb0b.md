

如果我们删除过滤器，setter 会显示一个空值。输入 **am**，我们会看到 setter 首先设置 **a**，然后设置 **am**。

Acme 产品管理

![](img/0155736aec718cf18821e9f10a5d308d_138_0.png)

每次用户输入时，值都会被设置，并且 setter 会被执行，将文本框中的值作为参数传入。只要你想在属性被获取或设置时执行代码，就可以使用 getter 和 setter。现在让我们看看如何利用这一知识来过滤我们的产品列表。

## Chapter 17 Filtering and Arrow Functions

我们正在朝着使用输入的过滤字符串来过滤产品列表的目标努力。我们的产品列表被定义为一个数组，因此我们可以使用 JavaScript 数组方法来处理我们的产品列表。

```
products: IProduct[] = [...];
```

要过滤我们的数组，我们使用 JavaScript 的 filter 方法。filter 方法会创建一个新数组。filter 方法随后会评估原始数组中的每个产品，以确定是否将其包含在新数组中。filter 方法然后返回新数组，只包含已过滤的产品。

```
performFilter(): IProduct[] {
  return this.products.filter();
}
```

不知如何，我们需要告诉 filter 方法我们希望用于确定产品是否满足过滤条件的逻辑。filter 方法期望我们的逻辑在产品应包含在过滤列表中时返回 true，否则返回 false。我们使用箭头函数来定义该逻辑。箭头函数是定义函数的紧凑语法。可以将其视为定义经典命名函数的更简短方式。它最常在向另一个函数或方法传递逻辑时使用。以下是将产品名称大写并返回的经典命名函数。

```
capitalizeName(product: IProduct): string {
  return product.productName.toUpperCase();
}
```

要将此代码写成箭头函数，我们忽略函数名，因为箭头函数不需要名称即可找到参数，然后是一个箭头。

```
(product: IProduct) => product.productName.toUpperCase();
```

这就是箭头函数得名的原因。我们忽略大括号和 return 关键字。具有单个语句的箭头函数具有隐含的主体和返回。然后我们编写所需的逻辑。如果箭头函数需要在函数主体中使用多个语句，则需要使用大括号和 return 关键字。

```
(product: IProduct) => {
  console.log(product.productName);
  return product.productName.toUpperCase();
}
```

只要你需要将一个函数传递给另一个函数或方法，就使用箭头函数。我们将在本书后面看到更多箭头函数。

```
performFilter(): IProduct[] {
  return this.products.filter((product: IProduct) =>
    product.productName.includes(this.listFilter));
}
```

现在让我们编写 performFilter 方法。我们将在下面与其它方法一起添加它。performFilter 方法接收 listFilter，它是一个字符串。该方法返回已过滤的产品数组。此代码首先将过滤条件转换为小写。为什么？这样我们在过滤产品列表时可以进行苹果对苹果的比较。我们想要一个比较。然后我们返回已过滤的产品列表。

我们从原始的完整产品列表开始，它是一个数组，因此我们可以使用任何 JavaScript 数组方法。我们想要使用 filter。我们将一个处理每个产品的箭头函数传递给 filter 方法。在箭头函数的主体中，我们检查 productName。由于我们将 listFilter 字符串小写了，我们也会将 productName 小写，以确保我们执行检查。然后我们调用字符串 includes 方法，将过滤字符串作为参数传入。includes 方法如果 productName 包含定义的过滤字符串则返回 true。因此，此代码将我们的产品列表过滤为仅产品名称包含列表过滤字符串的产品。如果列表过滤字符串为空，则返回所有产品。

```typescript
performFilter(filterBy: string): IProduct[] {
  filterBy = filterBy.toLocaleLowerCase();
  return this.products.filter((product: IProduct) =>
    product.productName.toLocaleLowerCase().includes(filterBy));
}
```

还有最后一步。我们需要更改我们的模板以绑定到我们的 filteredProducts 属性而不是我们的 products 属性。

```html
<tbody>
  <tr *ngFor='let product of filteredProducts'>
    <td>
      <img *ngIf='showImage'
           [src]='product.imageUrl'
           [title]='product.productName'
           [style.width.px]='imageWidth'
           [style.margin.px]='imageMargin'>
    </td>
```

## 一、翻译的标准

翻译是把一种语言所表达的思想内容用另一种语言准确、完整地重新表达出来的语言活动。翻译标准是翻译实践所遵循的准则，也是衡量译文好坏的尺度。翻译标准的确立对于翻译实践具有重要的指导意义。

我国近代翻译家严复提出了“信、达、雅”的翻译标准，对后世影响很大。“信”是指译文要忠实于原文的内容，“达”是指译文要通顺流畅，“雅”是指译文要典雅优美。这三者相互联系，不可分割。

## 二、翻译的方法

翻译的方法包括直译和意译两种。直译是既保持原文内容，又保持原文形式的翻译方法；意译是只保持原文内容，不保持原文形式的翻译方法。在实际翻译中，应根据不同的文体和语境灵活运用。

## 三、翻译的常用技巧

常用的翻译技巧包括增词法、减词法、词性转换法、分译法、合译法等。在具体翻译时，要结合上下文，灵活选用合适的技巧，使译文既忠实又通顺。

将 implements 关键字和接口名称添加到类的签名中。然后确保为接口中声明的每个属性和方法编写代码，以完全实现该功能。我们可以将组件的样式封装在组件本身中。

```
@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html',
  styleUrls: ['./product-list.component.css']
})
```

这样，组件所需的样式就与组件本身相关联，不会泄漏到应用程序的其它部分。使用 @Component 装饰器的 styles 属性来指定模板样式作为字符串数组。使用组件装饰器的 styleUrls 属性来标识外部样式表路径的数组。指定的样式随后会被封装在组件中。生命周期钩子允许我们深入组件的生命周期以执行操作。

```
import { Component, OnInit } from '@angular/core';

export class ProductComponent implements OnInit {
  ngOnInit(): void {
    console.log('In OnInit');
  }
}
```

使用生命周期钩子的步骤是：导入生命周期钩子接口，在组件类中实现生命周期钩子接口，然后为生命周期钩子接口中定义的钩子方法编写代码。

```
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'spacePipe'
})
export class SpacePipe implements PipeTransform {
    transform(value: string,
        character: string): string { ... }
}
```

要构建自定义管道，创建一个实现 PipeTransform 接口的类。此接口有一个方法。确保导出该类，以便管道可以从其它组件导入。在 Transform 方法中编写代码以执行所需的转换，并用 @Pipe 装饰器装饰该类。我们可以在任何模板中使用自定义管道，只要我们可以在其中指定管道。在 Angular 模块中，元数据在 declarations 数组中声明管道。然后与该 Angular 模块中声明的组件关联的任何模板都可以使用该管道。

```
@NgModule({
    imports: [...],
    declarations: [
        AppComponent,
        ProductListComponent,
        SpacePipe ],
    bootstrap: [ AppComponent ]
})
export class AppModule { }
```

在模板中，在要转换的属性之后立即输入管道字符，指定管道名称，并输入管道参数（如果有），以冒号分隔。

```
{{ product.productCode | spacePipe:'-' }}
```

我们现在已完成产品列表组件。接下来，我们将了解如何构建嵌套组件并构建星级组件。

## Chapter 18 How to Build Nested Components

我们的用户界面设计可能包含复杂到足以成为独立组件或在我们的视图中重复使用的功能。在本章中，我们将了解如何构建设计为嵌套在其它组件内的组件，并将发现如何建立嵌套组件与其容器组件之间的通信。就像套娃一样，我们可以嵌套我们的组件。我们可以将一个组件嵌套在另一个组件内，并将该组件嵌套在另一个组件内，以此类推。由于每个组件都是完全封装的，我们会为嵌套组件与其容器之间通信公开特定的输入和输出，使它们能够在两者之间传递数据。有两种方法可以使用组件并显示组件的模板。我们可以将组件用作指令。请回想一下，指令是我们用来增强 HTML 的自定义语法。当将组件用作指令时，我们使用组件选择器作为自定义 HTML 标签。我们在 index.html 文件中显示 AppComponent 模板时看到了如何将组件用作指令。指令被定义为 AppComponent 选择器。然后模板在指令标签内显示。我们对嵌套组件使用相同的技术。或者，我们可以将组件用作路由目标，这样用户看起来像是前往了另一个视图。然后模板在完整视图中显示。我们将在本书后面使用此技术路由到我们的产品列表视图。我们的产品列表视图目前用作指令，但这只是因为我们尚未涵盖路由。

