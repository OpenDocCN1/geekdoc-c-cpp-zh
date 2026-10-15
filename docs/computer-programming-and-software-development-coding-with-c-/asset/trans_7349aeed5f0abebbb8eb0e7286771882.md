

双花括号且不加引号。属性绑定将一个 HTML 元素属性设置为模板表达式的值。元素属性必须用方括号括起来，模板表达式则必须用引号括起来。事件绑定监听来自用户界面的事件，并在事件发生时执行组件方法。事件名称必须用圆括号括起来，事件发生时调用的方法也必须用引号括起来。双向绑定显示组件属性，并在用户在输入元素中进行更改时更新该属性。使用盒子里的香蕉语法配合 `ngModel` 指令。模板表达式必须用引号括起来。

![](img/0155736aec718cf18821e9f10a5d308d_113_0.png)

![](img/0155736aec718cf18821e9f10a5d308d_113_1.png)

![](img/0155736aec718cf18821e9f10a5d308d_113_2.png)

![](img/0155736aec718cf18821e9f10a5d308d_113_3.png)

使用 `ngModel` 时需要注意一些事项。在“盒子里的香蕉”语法中定义 `ngModel` 以实现双向绑定。

```html
<div class='col-md-4'>
  <input type='text'
         [(ngModel)]='listFilter' />
</div>
```

确保将 Angular 表单包中的 `FormsModule` 添加到适当的 Angular 模块（此处为 `AppModule`）的 imports 数组中。

```typescript
@NgModule({
  imports: [
    BrowserModule,
    FormsModule ],
  declarations: [
    AppComponent,
    ProductListComponent ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

这样可以确保 `ngModel` 指令可用于与该模块关联的任何组件中定义的模板。我们将在本书后面更详细地讨论 Angular 模块。组件中的数据类型可能不是我们想要显示的格式。我们可以在模板中使用管道（pipe）将数据转换为更合适的格式。要使用管道，请指定管道符号、管道名称以及任何管道参数，并用冒号分隔。在本章中，我们完成了更多 `ProductListComponent` 的内容，但它还可以更好。接下来，我们将看到几种改进组件的方法。接下来，我们学习几种改进组件的方法。组件是应用程序的关键构建块之一。我们让这些构建块更干净、更强壮、更耐用，应用程序就会更好，但如何让组件变得更好呢？强类型通过更好的语法检查和工具支持帮助减少错误。

## 第14章 如何定义接口

使用 TypeScript 的好处之一是其强类型。每个属性都有类型，每个方法都有返回类型，每个方法参数也都有类型。这种强类型通过更好的语法检查和工具支持帮助减少错误。然而，在某些情况下，我们的属性或方法没有预定义类型，比如这里的 products 数组。我们将 products 数组定义为 `any`，这削弱了强类型的好处。

```typescript
export class ProductListComponent {
  pageTitle: string = 'Product List';
  showImage: boolean = false;
  listFilter: string = 'cart';
  message: string;

  products: any[] = [...];

  toggleImage(): void {
    this.showImage = !this.showImage;
  }

  onRatingClicked(message: string): void {
    this.message = message;
  }
}
```

要指定自定义类型，我们可以定义一个接口。接口是一个规范，用于标识一组相关的属性和方法。

回想一下，属性是与类关联的数据元素，而方法执行类所需的逻辑。接口主要有两种使用方式。我们使用接口来标识特定类型的属性。在此示例中，我们定义了一个产品的属性。

```typescript
export interface IProduct {
  productId: number;
  productName: string;
  productCode: string;
  releaseDate: string;
  price: number;
  description: string;
  starRating: number;
  imageUrl: string;
}
```

然后我们可以将此接口指定为数据类型，以强化我们的代码类型。

```typescript
products: IProduct[] = [];
```

为任何需要的独特数据类型定义接口是一个好习惯。接口的第二种使用方式是标识一个功能集。

```typescript
export interface DoTiming {
  count: number;
  start(index: number): void;
  stop(): void;
}
```

我们声明实现特定功能所需的属性和方法。仅声明，不包含代码。在此示例中，我们定义了一个计时功能，包含 count 属性以及 start 和 stop 方法。要在组件中利用此功能，我们使用 `implements` 关键字指定接口。

```typescript
export class myComponent
    implements DoTiming {
  count: number = 0;
  start(index: number): void {
    ...
  }
  stop(): void {
    ...
  }
}
```

然后，我们为每个已定义的属性和方法编写代码。可以将此接口视为一个实现模式，详细说明特定功能所需的属性和方法。Angular 提供了一些接口形式的功能，我们通过实现这些接口来使用它们。实现接口的概念起初可能看起来有点令人生畏，但我们在本书的剩余部分会看到多个示例。现在，让我们专注于将接口用作数据类型。下面是一个 TypeScript 接口的示例。

```typescript
export interface IProduct {
    productId: number;
    productName: string;
    productCode: string;
    releaseDate: Date;
    price: number;
    description: string;
    starRating: number;
    imageUrl: string;
}
```

我们使用 `interface` 关键字定义接口，后面跟上接口名称，接口名称通常就是该接口所描述事物的名称。按照某些命名约定，接口会加上 I 前缀表示 interface（接口），不过许多 TypeScript 开发者会省略这个前缀。开头的 `export` 关键字导出了这个接口，从而使其可在应用程序的任何地方使用。接口的主体定义了这一类型适用的属性集。此示例定义了一个产品的属性。对于每个属性，接口都包含属性名、冒号和属性数据类型。一旦定义了接口，就可以将其用作数据类型。我们导入接口，然后将接口名称用作数据类型，就像使用 `string` 或 `boolean` 等其他数据类型一样。我们回到示例应用程序，查看 `ProductListComponent`。在这里，我们看到产品数组被定义为 `any`。那么让我们创建一个接口来定义产品到底是什么。我们将接口放到 products 文件夹中自己的文件里，并将该文件命名为 `product.ts`。首先输入 `export` 关键字，以确保应用程序的其他部分可以使用此接口。毕竟，这就是我们创建它的目的。接下来，输入 `interface` 关键字，然后是接口名称。我们正在定义一个产品，所以命名为 `IProduct`。在接口内部，我们定义属性。对于每个属性，我们定义属性名、冒号和属性类型。注意，我们将 `releaseDate` 类型设为 string。如果以后需要将此值作为日期对象处理，我们可以将该类型改为 date。

```typescript
export interface IProduct {
  productId: number;
  productName: string;
  productCode: string;
  releaseDate: string;
  price: number;
  description: string;
  starRating: number;
  imageUrl: string;
}
```

定义接口就这么简单。现在我们可以在 `ProductListComponent` 中使用此接口作为数据类型。不过，在这样做之前，我们先在产品数组中引入一个拼写错误。没有检测到错误。直到我们在浏览器中看到应用程序才发现错误。我们注意到其中一个产品没有显示图像。可以想象，这类错误可能会引发 bug。现在，我们用 `IProduct` 替换 `any`。出现了一个语法错误。我们遗漏了什么？嗯，我们需要一个导入语句。现在我们的产品数组已被强类型化，系统会通知我们在产品数组属性中犯了一个错误。我们甚至不必在浏览器中查看就能发现

