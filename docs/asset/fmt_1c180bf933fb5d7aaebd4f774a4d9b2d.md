
```typescript
import { Component } from '@angular/core';
import { IProduct } from './product';

@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html',
  styleUrls: ['./product-list.component.css']
})
export class ProductListComponent implements OnInit {
```

```
Add 'OnInit' to existing import declaration from "@angular/core"
Import 'OnInit' from module "@angular/core"
Learn more about JS/TS refactorings
```

现在我们这里又有另一个语法错误。

```typescript
import { Component, OnInit } from '@angular/core';
import { IProduct } from './product';

@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html',
  styleUrls: ['./product-list.component.css']
})
export class ProductListComponent implements OnInit {
```

```
Class 'ProductListComponent' incorrectly implements interface 'OnInit'.
Property 'ngOnInit' is missing in type 'ProductListComponent' but required in type 'OnInit'. ts(2420)
core.d.ts(4950, 5): 'ngOnInit' is declared here.
Peek Problem (Alt+F8)  Quick Fix... (Ctrl+.)
```

类 `ProductListComponent` 错误地实现了接口 `OnInit`。正如消息所述，现在我们已经实现了接口，我们必须为该接口中的每个属性和方法编写代码。`OnInit` 接口仅定义一个方法 `ngOnInit`，因此我们需要编写 `ngOnInit` 方法的代码。我们将在其他方法旁边添加它。由于我们目前不需要对它做任何事情，我们将只使用 `console.log` 将消息记录到控制台。

```typescript
ngOnInit(): void {
  console.log('In OnInit');
}
```

我们可以在浏览器中查看应用程序并使用 F12 开发工具打开控制台以查看记录的消息。

![](img/0155736aec718cf18821e9f10a5d308d_127_0.png)

我们将在本书后面使用 `ngOnInit`。接下来，我们将构建一个自定义管道。

## 第 16 章 如何构建自定义管道

正如我们之前看到的，我们使用管道在视图中显示之前转换绑定属性。有转换单个值或可迭代数据列表的管道。在本章中，我们想构建自己的自定义管道。对于我们的示例应用程序，产品代码以破折号存储并以这种方式显示，但用户更希望看到产品代码中用空格代替。我们可以构建一个自定义管道来用空格替换破折号，但让我们构建一个更通用的自定义管道，将字符串中任何指定的字符转换为空格。构建自定义管道所需的代码看起来在这一点上可能有些熟悉。

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
    name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {
    transform(value: string,
        character: string): string {
    }
}
```

它使用与我们在本书中创建的其他代码相似的模式。这里是类。我们向类添加管道装饰器以将其定义为管道。与我们使用过的其他装饰器类似，这是一个函数，因此我们添加括号。我们向函数传递一个对象，指定管道的名称。这是管道在

`AppModule` 中使用的名称。但如果我们有多个模块，我们会将其添加到声明需要该管道的组件的模块中。在我们的示例中，`ProductListComponent` 的模板需要该管道。因此我们将其声明添加到声明 `ProductListComponent` 的同一 Angular 模块中。我们在 `NgModule` 装饰器的 `declarations` 数组中定义管道。

```typescript
@NgModule({
  imports: [
    BrowserModule,
    FormsModule
  ],
  declarations: [
    AppComponent,
    ProductListComponent,
    ConvertToSpacesPipe
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

现在让我们构建我们的自定义管道。由于我们的自定义管道比较通用，我们将其添加到 `shared` 文件夹。我们将创建一个新文件并将其命名为 `convert-to-spaces.pipe.ts`，遵循我们的命名约定。首先，让我们编写类的代码：`export` 以便我们可以在需要的地方导入此管道，`class`，以及类名。我们将其命名为 `ConvertToSpacesPipe`。我们用 `Pipe` 装饰器装饰类并从 `@angular/core` 导入 `Pipe`。我们设置传递给 `Pipe` 装饰器的对象的 `name` 属性，定义管道的名称。这就是我们在 HTML 中引用管道时使用的名称。接下来，我们将实现 `PipeTransform` 接口。此语法错误是因为我们没有导入语句，所以让我们接下来添加它。

我们仍然有语法错误，因为当我们实现 `PipeTransform` 接口时，我们需要实现该接口中定义的所有属性和方法。

```typescript
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
  name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {

}
```

对于 `PipeTransform` 接口，只有一个方法 `transform`。我们将要转换的字符串值定义为第一个参数，将用于转换的字符字符串定义为第二个参数。我们可以添加一个 `return` 语句来消除这个最后一个语法错误。

```typescript
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({
  name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {

  transform(value: string, character: string): string {
    return '';
  }
}
```

现在我们希望 `transform` 方法做什么？我们的目标是用空格替换字符串中指定的任何字符。我们将使用 JavaScript 字符串 `replace` 方法将指定的字符替换为空格。就这样。

现在我们准备使用我们的管道了。在模板中，我们将管道添加到 `productCode` 上。但 `productCode` 本身已经有一个管道。没关系。我们可以添加任意数量的管道。首先指定管道名称，然后是任何管道参数。在本例中，我们想用空格替换破折号，所以我们在这里将破折号作为参数传入。

```html
<th>Product</th>
<th>Code</th>
<th>Available</th>
<th>Price</th>
<th>5 Star Rating</th>
</tr>
</thead>
<tbody>
<tr *ngFor="let product of products">
  <td>
    <img *ngIf="showImage"
      [src]="product.imageUrl"
      [title]="product.productName"
      [style.width.px]="imageWidth"
      [style.margin.px]="imageMargin">
  </td>
  <td>{{product.productName}}</td>
  <td>{{ product.productCode | lowercase | convertToSpaces:'-' }}</td>
  <td>{{ product.releaseDate }}</td>
  <td>{{ product.price | currency:'USD':'symbol':'1.2-2' }}</td>
  <td>{{ product.starRating }}</td>
</tr>
</tbody>
</table>
</div>

</div>
```

我们做完了吗？请记住，我们需要告诉 Angular 关于我们新的管道。我们通过在 Angular 模块中声明该管道来做到这一点。我们的 `ProductListComponent` 的模板想要使用 `convertToSpaces` 管道。所以我们打开声明了 `ProductListComponent` 的 Angular 模块，在我们的示例中是 `AppModule`。然后我们将 `ConvertToSpacesPipe` 添加到 `declarations` 中并添加所需的 `import`。

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { ProductListComponent } from './products/product-list.component';
import { ConvertToSpacesPipe } from './shared/convert-to-spaces.pipe';

@NgModule({
  declarations: [
    AppComponent,
    ProductListComponent,
    ConvertToSpacesPipe
  ],
  imports: [
    BrowserModule,
    FormsModule
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

现在 `AppModule` 中声明的任何组件都可以使用 `ConvertToSpacesPipe`。我们的产品代码现在显示为带空格而不是破折号。只要你需要执行数据转换，就构建一个自定义管道。然而，请注意，我们的页面交互性仍然不完整。产品列表尚未根据过滤条件进行过滤。让我们接下来看看这个问题。我们在这里有一个输入框供用户输入过滤字符串。然后产品列表应根据输入的字符串进行过滤。

## Acme 产品管理

### 产品列表

按以下过滤：cart

已过滤：cart

显示图片

|  | Product | Code | Available | Price | 5 Star Rating |

|---|---|---|---|---|---|

|  | Garden Cart | gdn 0023 | March 18, 2021 | $32.99 | 4.2 |

|  | Hammer | tbx 0048 | May 21, 2021 | $8.90 | 4.8 |

我们如何做到这一点？在回答这个问题之前，让我们花点时间谈谈 JavaScript 的 getter 和 setter。在 JavaScript 中，因此在 TypeScript 中，有两种方式在类中定义属性。

```ts
amount: number = 0;
```

我们可以像在这本书中之前所做的那样声明一个简单的变量作为属性。比喻地说，把这个简单变量属性想象成一个储蓄罐。我们可以直接把钱放进储蓄罐或从储蓄罐里取出钱。

```ts
get amount(): number {
    // process the amount
    // return amount from private storage
}
set amount(value: number) {
    // process the amount
    // retain amount in private storage
}
```

另一种定义属性的方式是使用 JavaScript getter 和 setter。把 getter 和 setter 想象成银行。我们把钱存入账户，银行处理金额，并把钱存放在某个私人的保险库中。当我们想要获取该金额时，银行需要先从私有存储中取出钱，然后才能返回该金额。在创建 getter 和 setter 时，我们通常会定义一个私有存储变量，称为 backing variable，用来存储由 getter 和 setter 管理的值。

```ts
private _amount: number = 0;
```

```ts
get amount(): number {
  // process the amount
  // return amount from private storage
  return this._amount;
}
set amount(value: number) {
  // process the amount
  // retain amount in private storage
  this._amount = value;
}
```

我们使用 `private` 关键字表示这个 backing variable 是私有的，只能由 getter 和 setter 管理。为了帮助我们识别这个变量为私有，按惯例我们用下划线作为前缀。在 getter 中，我们从私有存储返回金额，可选择在返回前处理该金额。例如，我们可以将值转换为另一种货币或格式化值。在 setter 中，我们将金额设置到私有存储中，可选择处理该金额。例如，我们可以记录金额或更新总余额。关键在于，通过使用 getter 和 setter 而不是简单变量作为属性，我们可以在获取或设置值时编写代码来处理该值。我们像访问简单变量属性一样访问这些属性，使用 `this` 引用类，然后是属性名。这里的代码将 200 设置到 `amount` 中，而这段代码获取 `amount` 并将其记录到控制台。这对我们和我们的过滤字符串意味着什么？如果我们为列表过滤器使用 getter 和 setter，我们就可以在每次设置过滤字符串时编写代码来过滤产品列表。因此，在实现列表过滤的第一步中，让我们将我们的 `listFilter` 属性改为 getter 和 setter。这里是我们的 `listFilter` 属性分配给默认值。我们希望在设置此属性时执行代码。让我们删除这个简单变量，改为构建一个 getter 和 setter。首先，我们声明一个私有 backing variable 来保存由 getter 和 setter 管理的值。我们在属性名前加上下划线以表示它是私有变量，并将其初始化为空字符串。接下来，我们定义 getter。getter 以 `get` 关键字开头，后跟属性名，放在括号中，并指定属性数据类型。getter 的主体可以包含在返回前处理属性值的代码。getter 然后返回处理后的值。由于我们不需要在获取时处理 `listFilter`，我们将返回 backing variable 的值。setter 以 `set` 关键字开头，后跟属性名。setter 有一个参数，即分配给属性的值。setter 没有返回值。setter 在任何时候为关联属性分配值时都会执行，因此我们可以使用 setter 的主体在属性更改时执行操作，例如过滤我们的产品列表。最小情况下，我们将值设置到私有 backing variable 中。我们将在下一步添加过滤列表的代码。现在，让我们只记录该值。请记住，我们原来的简单变量属性被分配了一个默认值。

```typescript
@Component({
  selector: 'pm-products',
  templateUrl: './product-list.component.html',
  styleUrls: ['./product-list.component.css']
})
export class ProductListComponent implements OnInit {
  pageTitle: string = 'Product List';
  imageWidth: number = 50;
  imageMargin: number = 2;
  showImage: boolean = false;

  private _listFilter: string = '';
  get listFilter(): string {
    return this._listFilter;
  }
  set listFilter(value: string) {
    this._listFilter = value;
    console.log('In setter:', value);
  }
}
```
