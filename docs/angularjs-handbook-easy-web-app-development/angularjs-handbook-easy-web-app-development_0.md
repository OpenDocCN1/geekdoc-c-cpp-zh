# AngularJS 手册：易于 Web 应用开发



![](img/00001.jpeg)




## 免责声明
尽管已尽一切努力验证书中提供的信息，但作者对书中包含的主题的错误、遗漏或相反的解释概不承担任何责任。书中提供的信息仅供教育和娱乐之用。读者应对自己的行为负责，作者对使用这些信息而导致的任何责任或损害（无论真实的还是感知的）均不承担任何责任。

所使用的商标均未经许可，且商标的发布未获得商标所有者的许可或支持。书中的所有商标和品牌仅用于说明目的，并归所有者所有，与本文档无关联。

# 第 1 章- AngularJS 概述
该框架通过对 HTML 提供的功能进行扩展来工作。如果 HTML 是为了开发 Web 应用而创建的，那么它应该是 AngularJS。在声明静态文档方面，HTML 是最好的。然而，对于我们 Web 应用中动态视图的声明，它并不理想。通过 Angular，你应用程序中使用的 HTML 词汇可以得到极大扩展。之后，你将获得一个易于阅读、具有表现力且开发速度更快的环境。

在书中，我们将探索 AngularJS 的各种功能，你作为开发者可以利用这些功能来改进应用程序的外观和体验。

# 第 2 章- AngularJS 与 HTML
如你所知，AngularJS 用于扩展 HTML 的功能。你们大多数人都知道如何使用标准 HTML。然而，AngularJS 用于扩展这些功能。在本章中，我们想要创建一个 HTML 页面，然后将 HTML 中编写的代码转换为模板，该模板将被 AngularJS 使用以动态显示相同的数据。HTML 页面中仅添加基本信息。

# 这里是网页的第一个段代码：
```html
<ul>
  <li>
    <span> Motorola </span>
    <p>
      I really like Motorola phones.
    </p>
  </li>
  <li>
    <span>Nokia are the best in Wi-Fi connection</span>
    <p>
      I really like to make use of devices.
    </p>
  </li>
</ul>
```

# 你可以继续在上面的文件中添加静态 HTML。下面给出了一个示例：
```html
<p> The number of available phones is: 2</p>
```

# 在示例中，我们刚刚使用了静态 HTML 来渲染刚刚创建的网页内容。通过 AngularJS，相同的内容可以动态渲染。

# 我们的目标是使我们创建的页面变为动态。还应该实现一个测试用例，以便对我们的控制器进行测试。在 AngularJS 中，MV 模型（模型-视图-控制器）用于组织应用程序的结构。通过这种方式，代码实现了解耦，并实现了关注点分离的概念。模型、视图和控制器将在此应用中添加。在 Angular 中发生的是模型通过视图投影到模板中。这表明如果发生某些变化，所有的绑定点都将更新，从而更新视图。视图在 Angular 中是从模型构建的。

# 考虑给出的示例：
```html
<html ng-app="myApp">
<head>
...
<script src="myapps/angular/angular.js"></script>
<script src="js/controllers.js"></script>
</head>
<body ng-controller="PhoneListCtrl">
  <ul>
    <li ng-repeat="model in phones">
      <span>{{model.name}}</span>
      <p>{{model.snippet}}</p>
    </li>
  </ul>
</body>
</html>
```

# 你所做的是将 `ng-repeat` 指令替换为控制器中硬编码的 `phones` 列表。如下所示：
```javascript
var myApp = angular.module('myApp', []);
myApp.controller('PhoneListCtrl', function ($scope) {
  $scope.phones = [
    {name: 'Motorola', snippet: 'I really like Motorola phones.'},
    {name: 'Nokia are the best in Wi-Fi connection', snippet: 'I really like to make use of devices.'}
  ];
});
```

## 测试
在 AngularJS 中，控制器和视图是分离的。通过这种方式，代码在开发期间也是可测试的。如果控制器在全局空间可用，我们可以模拟 `scope` 对象。示例所示：
```javascript
describe('PnListCtrl', function(){
  it(' a "phones" model with 2 phones, function() {
    var scope = {},
    ctrl = new PnListCtrl(scope);
    expect(scope.phones.length).toBe(2);
  });
});
```





随后应在文件中创建一个用于简单表格的重复器。可以通过以下方式实现：

```html
<table>
  <tr><th>行号 (the row number)</th></tr>
  <tr ng-repeat="j in [0, 1, 2, 3, 4, 5, 6, 7]"><<td>{{j}}</td></tr>
</table>_table>
```

然后应将列表修改为以下内容：

```html
<table>
  <tr><th>行号 (the row number)</th></tr>
  <tr ng-repeat="j in [0, 1, 2, 3, 4, 5, 6, 7]"><<td>{{j+1}}</td></tr>
</table_table>
```

`ng-repeat` 可用于创建具有其他规格的另一个表格。这在 `AngularJS` 中也非常强大。到此时，你将拥有一个动态运行的应用程序，并且它拥有模型（model）、视图（view）和控制器（controller），分别位于不同的位置。

# 第 3 章 - XHRs

你不总是要在应用程序中处理小规模且硬编码的数据。我们应该能够通过使用名为 `$http` 的预构建服务从我们的 `AngularJS` 服务器获取大型数据集。

我们将有一个文件 `app/phones/devices.json`，其中包含了我们拥有的手机列表。这些将以 JSON 格式存储。该文件的一个示例如下：

```json
[
{
  "age": 15,
  "id": "motorola ",
  "name": "Motorola DEFY\u2122 with MOTOBLUR\u2122",
  "snippet": "Do you enjoy using Motorola devices and phones?"
...
},
...
]
```

## 控制器 (Controller)

`Angular` 的 `$http` 服务将在控制器用于向 Web 服务器发送 HTTP 请求，以便从 `app/phones/devices.json` 获取数据。这是处理此类问题或与 Web 应用相关操作的方法之一。在 `AngularJS` 中，这些服务会被注入到需要的地方。

控制器的代码如下所示：

```javascript
var myApp = angular.module('myApp', []);
myApp.controller('PnListCtrl', function ($scope, $http) {
  $http.get('phones/devices.json').success(function(data) {
    $scope.phones = data;
  });
  $scope.orderProp = 'age';
});
```

若要在 `Angular` 中使用服务，必须将所需的依赖项名称定义为控制器构造函数的参数。如下：

```javascript
myApp.controller('PnListCtrl', function ($scope, $http) {...}
```

`AngularJS` 中的依赖构造函数将在启动后为我们的控制器提供服务。服务可能具有任何间接依赖的创建过程也会被处理。考虑下面的示例，它展示了如何实现：

```javascript
var myApp = angular.module('myApp', []);
myApp.controller('PnListCtrl', ['$scope', '$http',
function ($scope, $http) {
  $http.get('phones/devices.json').success(function(data) {
    $scope.phones = data;
  });
  $scope.orderProp = 'age';
}]);
```

测试可以如下方式进行：

```javascript
describe('myApp controllers', function() {
describe('PnListCtrl', function(){
  var scope, ctrl, $httpBackend;
  // 在测试之前加载我们的模块定义。
  beforeEach(module('myApp'));
  // 注入器在这里会忽略前导和尾的下划线（即 _$httpBackend_）。
  // 这允许我们注入服务，同时也将其附加到变量上，
  // 变量名与服务相同，以避免名称冲突。
  beforeEach(inject(function(_$httpBackend_, $rootScope, $controller) {
    $httpBackend = _$httpBackend_;
    $httpBackend.expectGET('phones/devices.json').
    respond([{name: 'Motorola'}, {name: 'Motorola Phone'}]);
    scope = $rootScope.$new();
    ctrl = $controller('PnListCtrl', {$scope: scope});
  }));
```

注意上述测试用例中的两个辅助函数。它们可以用于配置和访问注入器。

考虑下面的代码：

```javascript
it('你应该创建一个 "phones" 模型，包含 2 个从 xhr 获取的手机', function() {
  expect(scope.phones).toBeUndefined();
  $httpBackend.flush();
  expect(scope.phones).toEqual([{name: 'Motorola'},
  {name: 'Motorola Phone'}]);
});
```

我们希望在接收到响应之前，对 scope 上不存在的模型进行验证。在调用函数 `$httpBackend.flush()` 后，请求队列将刷新到浏览器。由服务 `$http` 返回的 promise 将用我们的解析响应被解析。我们将进行断言，然后验证模型是否属于 scope。然后我们可以验证 `orderProp` 是否已正确设置。如下所示：

```javascript
it('默认值应该被设置', function() {
  expect(scope.orderProp).toBe('age');
});
```

在 `Angular` 中，观察到以下内容：
`<pre>{{phones | orderProp}}</pre>`

输出应该是：
`$scope.devices = data.splice(0, 5);`

# 第 4 章 - 链接与图片 (Images)

你应该知道如何为设备添加图片。注意在 JSON 文件中 URL 是可用的。考虑以下代码：

```json
{
  "id": "motorola ",
  "imageUrl": "img/phones/motorola.jpg",
  "name": "Motorola "
}
```

模板应该是：

```html
<ul class="phones">
  <li ng-repeat="device in phones | query | orderProp" class="thumbnail">
    <a href="#phones/{{device.id}}" class="thumb"><img ng-src="{{device.imageUrl}}"></a>
    <a href="#phones/{{device.id}}">{{device.name}}</a>
    <p>{{device.snippet}}</p>
  </li>
</ul>
```

链接的测试可以如下实现：

```javascript
it('渲染特定的链接', function() {
  var myquery = element(by.model('query'));
  myquery.sendKeys('nexus');
  element.all(by.css('.phones a')).first().click();
  browser.getLocationAbsUrl().then(function(url) {
    expect(url).toBe('/phones/motorola');
  });

# 第 5 章 - 使用动画

有时你可能需要通过添加动画来增强应用程序。这可以通过 CSS 和 JavaScript 实现。为了在整个应用程序中启用动画，我们必须使用 `ngAnimate` 模块。常用的 `ng` 指令用于触发我们正在接入的动画钩子。这应该是自动完成的。一旦找到动画，它将在该时间发布的标准 DOM 元素之间执行。`ngRepeat` 和 `ngClass` 可以用于此，只需向它们添加或删除元素即可。

我们现在需要安装应用程序客户端使用的依赖项。Bower 可用于此目的。我们需要更新配置文件 `bower.json` 以包含新的依赖项。




```json
{
  "angular-mocks": "1.4.x",
  "jquery": "~2.1.1",
  "bootstrap": "~3.1.1",
  "angular-route": "1.4.x",
  "angular-resource": "1.4.x",
  "angular-animate": "1.4.x"
}
```

上一步中安装的所有元素都应该是兼容的，否则将会出现问题。已经指示 bower 安装了 jQuery。然而，这不能称它为 Angular 库，但它是一个标准的 jQuery 库。

执行以下命令指示 bower 下载并安装依赖项：

```
npm install
```

请注意，如果在您上次执行上述命令之后发布了新版本的 Angular，可能会出现不兼容的情况。要解决这个问题，您只需要在再次执行上述命令之前删除 `app/bower_components` 文件夹即可。

## 模板 (The Template)

我们必须对 HTML 模板进行一些更改，以便链接定义动画的资源文件以及 `angular-animate.js` 文件。动画模块（即 `ngAnimate`）定义在该文件中，它包含了负责让应用程序感知动画效果的代码。

必须对该文件进行以下更改：

```html
<!--此用于 CSS 过渡和/或关键帧动画 -->
<link rel="stylesheet" href="css/animations.css">

<!--- jQuery 将用于 JavaScript 动画（这应该包含在 angular.js 之前） -->
<script src="bower_components/jquery/dist/jquery.js"></script>

<!---这是在 AngularJS 中启用动画支持所需的模块 -->
<script src="bower_components/angular-animate/angular-animate.js"></script>

<!-此用于 JavaScript 动画 -->
<script src="js/animations.js"></script>
```

对于使用 Angular 1.4 版本的用户，请确保您正在使用 jQuery 2.1 及以上版本。任何低于此的版本都将与 Angular 1.4 不兼容。这意味着动画将无法检测到，或者可能会以不符合预期的方式运行。

动画可以在 CSS 代码 (`animations.css`) 中或在 JavaScript 代码 (`animations.js`) 中实现。我们需要首先创建一个新模块，该模块将像我们在 `ngResource` 中做的那样，将 `ngAnimate` 模块作为依赖项。

`animations.js` 文件应如下：

```javascript
angular.module('myAnimations', ['ngAnimate']);
  // ...
// 此模块稍后用于定义动画
  // ...
```

然后将该模块附加到应用程序模块上。如下所示：

```javascript
angular.module('myApp', [
  'ngRoute',
  'myAnimations',
  'myControllers',
  'myFilters',
  'myServices',
]);
```

此时，我们的模块就会被识别了。

## 使用 CSS 过渡动画的 ng-Repeat 动画

应该将 CSS 动画添加到包含我们设备的网页中的 `ngRepeat` 指令中。我们应该首先为被重复的元素添加一个额外的 CSS 类，以便它可以与 CSS 动画代码挂钩。如下所示：

```html
<!-- 更改重复器的 HTML 以包含一个新的 CSS 类
     我们稍后将将其用于动画： -->
<ul class="phones">
  <li ng-repeat="device in phones | filter:query | orderBy:orderProp" class="thumbnail device-listing">
    <a href="#/phones/{{device.id}}" class="thumb"><img ng-src="{{device.imageUrl}}"></a>
    <a href="#/phones/{{device.id}}">{{device.name}}</a>
    <p>{{device.snippet}}</p>
  </li>
</ul>
```

注意 CSS 类是如何添加的。这在 HTML 文件中是必要的，这样动画才能正常工作。动画的 CSS 代码应如下：

```css
.device-listing.ng-enter,
.device-listing.leave,
.device-listing.move {
  -webkit-transition: 0.5s all;
  -moz-transition: 0.5s all;
  -o-transition: 0.5s all;
  transition: 0.5s all;
}
.device-listing.ng-enter,
.device-listing.move {
  opacity: 0;
  height: 0;
}
.device-listing.ng-move-active,
.device-listing.ng-enter.enter-active {
  opacity: 1;
  height: 20px;
}
.device-listing.leave {
  opacity: 1;
  overflow: hidden;
}
.device-listing.leave.leave-active {
  opacity: 0;
  height: 0;
  padding-top: 0;
  padding-bottom: 0;
}
```

`device-listing` 的 CSS 类已与项目在插入和从列表中移除时会发生的动画钩子结合。`ng-enter` 将在新设备添加到列表并显示在页面之后应用到该元素上。`ng-move` 将元素在列表中移动后应用。`ng-leave` 将在元素从列表中移除后应用。

## ngView 的动画

我们现在需要为 `ngView` 中路由更改之间的过渡添加动画。必须像我们在之前的示例中做的那样，在 HTML 中添加一个新的 CSS 类。除了添加到 `ngRepeat` 元素中，我们还将其添加到 `ngView` 中。这意味着 HTML 代码需要进行一些更改。这意味着视图之间的动画将更具可性。`index.html` 文件应如下：

```html
<div class="view-container">
  <div ng-view class="view-frame"></div>
</div>
```

使用了 `view-container` CSS 类将 `ng-view` 指令嵌套在父元素内部。该类将添加 `position: relative` 样式，以便在过渡进行动画时，`ng-view` 指令的位置相对于父元素。过渡的 CSS 应该添加到 `animation.css` 文件中。如下所示：

```css
.view-container {
  position: relative;
}
.view-frame.ng-enter, 
view-frame.ng-leave {
  background: white;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
}
.view-frame.ng-enter {
  -webkit-animation: 0.5s fade-in;
  -moz-animation: 0.5s fade-in;
  -o-animation: 0.5s fade-in;
  animation: 0.5s fade-in;
  z-index: 100;
}
.view-frame.ng-leave {
  -webkit-animation: 0.5s fade-out;
  -moz-animation: 0.5s fade-out;
  -o-animation: 0.5s fade-out;
  animation: 0.5s fade-out;
  z-index: 99;
}
@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}
@-moz-keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}
@-webkit-keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}
@keyframes fade-out {
  from { opacity: 1; }
  to { opacity: 0; }
}
@-moz-keyframes fade-out {
  from { opacity: 1; }
  to { opacity: 0; }
}
@-webkit-keyframes fade-out {
  from { opacity: 1; }
  to { opacity: 0; }
}
```

/* 不要忘记厂商前缀 */
## 使用 JavaScript 的 ngClass 动画

我们需要为我们的应用程序添加另一个动画。在 `device-list.html` 页面将观察到一个漂亮的缩略图。一旦点击缩略图，图像就会更改。必须更改 CSS 类以确保图像显示是准确的。如下所示：

```css
.phone-images {
  background-color: white;
  width: 450px;
  height: 450px;
  overflow: hidden;
  position: relative;
  float: left;
}

...

img.device {
  float: left;
  margin-right: 3em;
  margin-bottom: 2em;
  background-color: white;
  padding: 2em;
  height: 400px;
  width: 400px;
  display: none;
}

img.device:first-child {
  display: block;
}
```

你认为我们将创建一个启用 CSS 的动画。然而，我们可以通过使用 JavaScript 的 `animation()` 模块来实现。如下文示例所示：





```javascript
var myAnimations = angular.module('myAnimations', ['ngAnimate']);

myAnimations.animation('.device', function() {
  var animUp = function(element, cName, done) {
    if(cName != 'active') {
      return;
    }
    element.css({
      position: 'absolute',
      top: 500,
      left: 0,
      display: 'block'
    });
    jQuery(element).animate({
      top: 0
    }, done);
    return function(cancel) {
      if(cancel) {
        element.stop();
      }
    };
  }
  var animDown = function(element, cName, done) {
    if(cName != 'active') {
      return;
    }
    element.css({
      position: 'absolute',
      left: 0,
      top: 0
    });
    jQuery(element).animate({
      top: -500
    }, done);
    return function(cancel) {
      if(cancel) {
        element.stop();
      }
    };
  }
  return {
    addClass: animUp,
    removeClass: animDown
  };
});
```

正如你所注意到的，动画是通过使用 `jQuery` 实现的。通过 Angular 和 JavaScript，我们不需要使用 `jQuery` 来执行动画。在 JavaScript 中编写自己的动画库是非常的。

# 第 6 章- `$watch()`, `$digest()` 和 `$apply()`

这些方法在 AngularJS 中被广泛使用。你应该学习如何在 Angular 中使用它们。

在视图的某处对对象“$scope”上的变量创建了数据绑定后，Angular 内部会创建一个“监听（watch）”。通过这个监听器，意味着它将监控“$$scope”对象中的内容。这表明框架正在监控该变量。要创建监听器，我们使用 `$scope.$watch()` 函数。

在大多数情况下，`$scope.$digest()` 和 `$scope.$watch()` 函数会替你调用，但在其他情况下，你可能需要手动调用它们。这就是为什么你应该知道并理解它们是如何工作的。

`$scope.$apply` 函数用于执行特定的代码，并在之后调用 `$scope.$digest()` 函数。这将检查所有的监听器，并调用所有对应的监听器回调函数。`apply()` 函数在将 AngularJS 代码与任何其他代码集成时非常有用。

## `$watch()`

`$scope.watch()` 函数用于创建特定变量的监听器。一旦注册了监听器，必须向 `$watch()` 函数传递两个参数。这两个参数包括：

*   一个值函数（value function）
*   一个监听函数（listener function）

考虑下面的示例，展示如何实现：

```javascript
$scope.$watch(function() {},
      function() {}
);
```

第一个函数代表值函数，而第二个函数代表监听函数。通过值函数将返回被监控的值。随后，由 AngularJS 来将返回的值与上一次监听函数返回的值进行比较。AngularJS 改变了检查是否返回了值的方法。下例所示：

```javascript
$scope.$watch(function(scope) { return scope.data.myVariable },
      function() {}
);
```

使用上述函数，值函数将返回 `scope.data.myVariable` 的值。如果该变量的值发生了变化，则必须返回一个不同的值。随后 AngularJS 将调用监听函数。

如果值发生了变化，监听函数将尝试尽其所能的操作。通过使用此值，值函数可以访问 `$scope` 及其变量。在需要时，值函数也可以监控全局变量，但大多数情况下监控的是 `$scope` 变量。

如果值发生了变化，监听函数可以执行任何它需要的操作。对于某些人来说，他们可能需要更改变量的内容，而另一些人可能需要更改 HTML 元素的内容。考虑下面的示例：

```javascript
$scope.$watch(function(scope) { return scope.data.myVariable },
function(nValue, oValue) {
    document.getElementById("").innerHTML =
      "" + newValue + "";
}
);
```

上面的示例将把 HTML 元素的 `innerHTML` 设置为变量的新值，并且这被嵌入在“b”元素中以使内容加粗。

## `$digest()`

`$scope.$digest()` 函数将遍历“$scope”对象和子“$scope”对象中的所有监听器。当 `$digest()` 函数遍历完监听器后，框架会更新数据绑定。

## `$apply()`

`$scope.$apply` 函数用于执行特定的代码，并在之后调用 `$scope.$digest()` 函数。这将检查所有的监听器。我们为应用程序创建了两个按钮。第一个按钮绑定了一个类型为 `ng-click` 的监听器。点击此按钮将调用该函数。

考虑下面的示例：

```html
<div ng-controller="appController">
  {{data.time}}
  <br/>
  <button ng-click="updateTime()">update time - ng-click</button>
  <button id="upTime">change time</button>
</div
```

```javascript
var module = angular.module("myapplication", []);

var appController = module.controller("appController", function($scope) {
  $scope.data = { time: new Date() };

  $scope.updateTime = function() {
    $scope.data.time = new Date();
  }

  document.getElementById("upTime")
  .addEventListener('click', function() {
    console.log("change time clicked");
    $scope.data.time = new Date();
    $scope.$digest();
  });
});
```





与其执行上述操作（即在事件监听器内部调用 `$digest()` 函数），也可以像下面所示使用 `apply()` 函数：

```javascript
document.getElementById("upTimeButton")
  .addEventListener('click', function() {
    $scope.$apply(function() {
      console.log("change time clicked");
      $scope.data.time = new Date();
    });
  });
```

函数 `$scope.$apply()` 在按钮的事件监听器内部被调用，变量 `$scope.data.time` 的更新已作为参数传递给 `$apply()` 函数。一旦 `$apply()` 函数执行完毕，AngularJS 将在内部调用 `$digest()` 函数，以便对所有数据绑定进行更新。

# 第 7 章 - "$scope" 的层级结构

视图使用的 AngularJS `$scope` 对象被组织成一个层级结构。我们从根作用域（root scope）开始，它由一个或多个子作用域组成。每个可用视图由自己的作用域组成，该作用域只是根作用域的子级。这意味着视图控制器在 `$scope` 上设置的变量对其他控制器都是不可见的。

考虑下面提供的 AngularJS 代码作为示例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.2.5/angular.min.js"></script>
</head>
<body ng-app="myapplication">
  <div ng-controller="appController1">
    {{data.theVariable}}
  </div>
  <div ng-controller="appController2">
    {{data.theVariable}}
  </div>
  <script>
    var module = angular.module("myapplication", []);
    var appController1 = module.controller("appController1", function($scope) {
      $scope.data = { theVariable : "first value"};
    });
    var appController2 = module.controller("appController2", function($scope) {
      $scope.data = { theVariable : "second value"};
    });
  </script>
</body>
</html>
```

在上面的示例中，我们使用了两个视图，每个视图都有自己的控制器。每个控制器都会将 `data.theVariable` 变量设置为不同的值。

一旦程序执行，你将获得以下层级结构：

- 根 `$scope`
- appController 1 的 `$scope`
- appController 2 的 `$scope`

如所示，两个视图使用了不同的作用域对象。通过此示例，我们的两个视图内部的 `{{data.theVar}}` 数据绑定也将写入两个不同的值。`$scope` 对象中的变量 `data.theVariable` 也会被设置为不同的值。

# 第 8 章- 重构 AngularJS 应用

基于组件的指令（Directives）在 AngularJS 中变得越来越流行。这是因为组件带来了易用性。然而，目前使用的大多数 Angular 应用并不是基于组件的。

对于 Angular2 用户，可以按照以下方式使用组件：

```html
<confirmation
    [message]="'Start firing?'"
    (ok)="startFiring()">
</confirmation>
```

如上面的示例所示，组件只是 HTML 中的一个元素，它匹配在其他处定义的组件名称。每个组件都有自己的输入和输出，这些是作为属性提供给元素的。

上面的组件也可以如下所示定义：

```typescript
@Component({
  selector: 'confirmation',
  properties: ['message'],
  events: ['ok']
})
@View({
  template: `
    <div>
      {{message}}
      <button (click)="ok()">OK</button>
    </div>
  `
})
class Confirmation {
  okEvents = new EventEmitter();
  ok() {
    this.okEvents.next();
  }
}
```

使用接口边界来规范组件可以处理的输入和输出。UI 模板被用于为用户定义接口。组件逻辑隐藏在 UI 模板之后，用于定义组件的行为以及当用户与其交互时的操作。将组件定义为指令可以如下所示：

```typescript
@Component({
  selector: 'confirmation',
  properties: ['message'],
  events: ['ok']
})
@View({
  template: `
    <div>
      {{message}}
      <button (click)="ok()">OK</button>
    </div>
  `
})
class Confirmation {
  okEvents = new EventEmitter();
  ok() {
    this.okEvents.next();
  }
}
```

上面的代码与我们之前的完全不同。在 AngularJS 中可以很容易地完成或使用使用重构。我们想提供一个关于如何操作的示例：

考虑下面文件 `index.html` 的代码：

```html
<div ng-include="'bar.html'"></div>
```

为了替换上述内容，我们必须为 `bar` 创建一个指令。这将使用继承的作用域和 ` `bar.html` 模板。`bar_directive.js` 的代码如下：

```javascript
module.directive('bar', function() {
  return {
    scope: true,
    templateUrl: 'bar.html'
  };
});
```

为了让其有效工作，指令和模板必须位于同一位置，并且它们的名称也应该匹配。如下所示：

`components/foobar/`
- `bar_directive.js`
- `bar.html`

原始的 `ng-include` 应该被新指令替换。如下所示：

```html
<div ng-include="'footbar.html'"></div>
<footbar></footbar>
```

在添加上述组件指令（即 `footbar`）之后，模板本身将如下所示：

```html
<div ng-controller="FoobarCtrl as c">
  <p>{{c.getText()}}</p>
</div>
```

我们接着想要移动并重命名包含 FootCtrl 的文件，使其与我们的组件指令位于同一位置。如下所示：

`components/foobar/`
- `bar_directive.js`
- `bar_controller.js`
- `bar.html`

然后应该在指令中使用控制器，并使用与我们的 `ng-controller` 相同的 `ctrl` 别名。文件 `bar_directive.js` 如下：

```javascript
module.directive('bar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    templateUrl: 'bar.html'
  };
});
```

现在可以从模板中移除 `ng-controller`。如下所示：

```html
<div ng-controller="FoobarCtrl as c">
  <p>{{c.getText()}}</p>
</div>
```

我们也可以选择保留此元素用于样式设置。考虑以下示例：

```html
<div ng-controller="FoobarCtrl as c">
  <p>{{c.getText()}}</p>
</div>
```

在上述表示模板的示例中，我们有一个 `ng-controller`。我们需要创建一个新的指令。这应该创建一个继承的作用域，并使用 `FoobarCtrl` 然后将其别命名为 `c`。如下所示：

```javascript
module.directive('bar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c'
  };
});
```

我们的新指令和控制器将移动到相同的位置。它们应该具有相同的前缀。如下所示：

`components/foobar/`
- `bar_directive.js`
- `bar_controller.js`

最后，在原始模板中，可以将 `ng-controller` 替换为组件 `footobar` 的实例。如下所示：

```html
<div ng-controller="FoobarCtrl as c" class="foo-bar">
  <footbar class="foo-bar">
    <p>{{c.getText()}}</p>
  </footbar>
</div>
```

这是我们现在拥：

```html
<div ng-controller="FoobarCtrl as c" class="foo-bar">
  <footbar class="foo-bar">
    <p>{{c.getText()}}</p>
  </footbar>
</div>
```

应该应该为组件指令创建一个模板文件。如下所示：

`components/foobar/`
- `bar_directive.js`
- `bar_controller.js`
- `bar.html`

新模板应该从指令中引用。可以如下所示操作：

```javascript
module.directive('footobar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    templateUrl: 'bar.html'
  };
});
```

我们将使用指令元素中包含的内容来填充新模板。如下所示：

```html
<p>{{c.getText()}}</p>
```




指令元素本身将变为空。`index.html` 文件将如下所示：

```html
<foobar>
<p>{{c.getText()}}</p>
</foobar>
```

当 `ng-controller` 被替换为指令后，原始模板将剩下以下内容：

```html
<foobar>
<h2>{{c.getTitle()}}</h2>
<p>{{mainC.getText()}}</p>
</foobar>
```

转体（Transclusion）可以被用于同时支持这两种情况。我们将开始为我们的组件指令创建一个模板文件。如下所示：

`components/foobar/`
*   `bar_directive.js`
*   `bar_controller.js`
*   `bar.html`

然后我们可以在我们的指令中引用新模板。同时，也将启用转体，如下所示：

```javascript
module.directive('foobar', function() {
  return {
    transclude: true,
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    templateUrl: 'bar.html'
  };
});
```

模板文件的填充将通过使用原始模板中需要放入组件内部的部分来实现。对于另一部分，将添加 `ng-transclude` 指令。`bar.html` 文件应该包含以下代码：

```html
<h2>{{c.getTitle()}}</h2>
<p ng-transclude></p>
```

在我们的指令元素中，我们将保留需要被转体的部分。如下所示：

```html
<foobar>
<h2>{{c.getTitle()}}</h2>
<p>{{mainC.getText()}}</p>
</foobar>
```

考虑下一个示例。

我们有一个用于列出某些数据的 `<ul>` 元素。如下所示：

```html
<div>
  <h1>Foobars</h1>
  <ul>
    <li ng-repeat="foo in c.bars">
      <img ng-src="foo.imageUrl"/>
      {{file.text}}
    </li>
  </ul>
</div>
```

我们需要将该列表提取到它自己的组件中。应该为该组件创建一个指令和一个模板文件。在指令中应这样调用它，如下所示：

`components/foobar_list/`
*   `foobar_list_directive.js`
*   `foobar_list.html`

指令将创建一个继承作用域，然后引用已创建的模板。如下所示：

```javascript
module.directive('foobarList', function() {
  return {
    scope: true,
    templateUrl: 'list.html'
  };
});
```

模板的填充将通过复制从我们原始模板中填充的 HTML 文件来实现。如下所示：

```html
<ul>
  <li ng-repeat="foo in c.bars">
    <img ng-src="foo.imageUrl"/>
    {{file.text}}
  </li>
</ul>
```

随后可以在原始模板中使用该组件的新实例。它将替换掉已创建的标记。如下所示：

```html
<div>
  <h1>Foobars</h1>
  <ul>
    <li ng-repeat="foo in c.bars">
      <img ng-src="foo.imageUrl"/>
      {{file.text}}
    </li>
  </ul>
  <foobar-list></foobar-list>
</div>
```

也可以创建一个利用转体的示例。下给出了该示例：

```html
<div>
  <h1>Foobars</h1>
  <ul>
    <li ng-repeat="foo in c.bars">
      <h3>
        {{mainC.itemHeader}}
      </h3>
      <img ng-src="foo.imageUrl"/>
      {{file.text}}
    </li>
  </ul>
</div>
```

我们上一个示例中的 `<ul>` 元素包含来自外部的内容，转体可以被用于这两种目的。在上面的示例中，我们使用了由 `mainC` 提供的项目头部。

当列表提取到它自己的组件时，应该为该文件创建一个指令和一个模板。如下所示：

`components/foobar_list/`
*   `bar_list_directive.js`
*   `bar_list.html`

指令将创建一个继承作用域，然后引用新创建的模板文件。也将启用转体。

`bar_list_directive.js` 文件的代码如下：

```javascript
module.directive('foobarList', function() {
  return {
    transclude: true,
    scope: true,
    templateUrl: 'bar_list.html'
  };
});
```

模板的填充将通过复制从我们原始模板中提取的 HTML 来。项目头部的部分将被 `ng-transclude` 元素替换。

`bar_list.htm` 的代码如下：

```html
<ul>
  <li ng-repeat="foo in c.bars">
    <ng-transclude></ng-transclude>
    <img ng-src="foo.imageUrl"/>
    {{file.text}}
  </li>
</ul>
```

随后可以在我们的新模板中使用该组件的新实例。它将替换掉已提取的标记，但会留下项目头部。如下所示：

```html
<div>
  <h1>Foobars</h1>
  <ul>
    <li ng-repeat="foo in c.bars">
      <img ng-src="foo.imageUrl"/>
      {{file.text}}
    </li>
  </ul>
</div>
```



外部引用不仅可以在组件模板中找到。在组件控制器中，可能还会包含表达式 `"$watch,"`、`"$watchCollection,"` 或 `"$watchGroup."`。如果可用，也可以使用链接函数。考虑下面的示例，它展示了如何将其替换为绑定的输入：

```javascript
function FoobarCtrl($scope) {
  var c = this;
  $scope.$watch('mainC.foo', function(nFoo) {
    if (nFoo.active) {
      ctrl.actFoo = nFoo;
    } else {
      c.actFoo = null;
    }
  });
}
```

我们的监听表达式引用了 `"mainC."` 的 `"foo"` 属性。应该使用绑定的输入代替它。考虑下面的代码：

```javascript
module.directive('foobar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    bindToController: {
      foo: '='
    },
    templateUrl: 'bar.html'
  };
});
```

一旦组件被使用，就应该接入实际值。如下所示：

```html
<foobar foo="mainC.foo">
</foobar>
```

在控制器的监听表达式内部，就可以使用绑定的输入了。如下所示：

```javascript
function FoobarCtrl($scope) {
  var c = this;
  $scope.$watch('c.foo', function(nFoo) {
    if (nFoo.active) {
      ctrl.actFoo = nFoo;
    } else {
      c.actFoo = null;
    }
  });
}
```

在某些情况下，不能使用外部引用。我们想为控制器创建代码，该代码将引用一段仅在纯 JavaScript 中继承的作用域属性的代码。这里是该示例的代码：

```javascript
function FoobarCtrl($scope) {
  var c = this;
  c.getActiveFoo = function() {
    if ($scope.mainC.foo.active) {
      return $scope.mainC.foo;
    } else {
      return null;
    }
  };
}
```

上面的示例与上一个相似，唯一的区别是需要一个绑定的输入。如下所示：

```javascript
module.directive('foobar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    bindToController: {
      foo: '='
    },
    templateUrl: 'bar.html'
  };
});
```

`foo` 值将在使用组件时被提供。如下所示：

```html
<foobar foo="mainC.foo">
</foobar>
```

我们的控制器代码随后将能够使用绑定的输入。如下所示：

```javascript
function FoobarCtrl($scope) {
  var c = this;
  ctrl.getActiveFoo = function() {
    if (c.foo.active) {
      return c.foo;
    } else {
      return null;
    }
  };
}
```

## 事件处理器和绑定输出

组件中使用的所有外部组件并非逻辑输入。其他的则作为逻辑输出。考虑下面的示例：

```html
<div ng-show="c.visible">
  <p>{{c.getText(c.language)}}</p>
  <button ng-click="mainC.deleteFoobar()">
    Delete
  </button>
</div
```

在上面的示例中，在我们的组件模板内部，我们有 `"ng-click"` 指令。它被用于调用已继承的 `"mainC"` 引用上的方法。这就是我们所做的。

为了打破依赖，必须在指令的定义上引入一个名为 `"onDelete"` 的表达式绑定。如下所示：

```javascript
module.directive('foobar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    bindToController: {
      visible: '=',
      language: '=',
      onDelete: '&'
    },
    templateUrl: 'bar.html'
  };
});
```

在 AngularJS 中，为了区分输入和输出，`[]` 语法用于输入，`()` 语法用于输出。然而，在 AngularJS 的早期版本（如 `1.x`）中，没有区分这些者的机制。这就是为什么大多数人倾向于为输出使用 `"on"` 前缀。

一旦组件被使用，就会为新绑定接入表达式。组件的用户将决定删除对他/她意味着什么。在我们的案例中，我们使用它是调用主控制器的 `"deleteFoobar"` 函数。如下所示：

```html
<foobar
  visible="mainC.isFooBarVisible()"
  language="mainC.getLanguage()"
  onDelete="mainC.deleteFoobar()">
</foobar>
```

该表达式绑定将从组件模板内部被调用。如下所示：

```html
<div ng-show="c.visible">
  <p>{{c.getText(c.language)}}</p>
  <button ng-click="c.onDelete()">
    Delete
  </button>
</div
```

考虑下面的示例代码：

```javascript
function FoobarCtrl($scope) {
  var c = this;
  c.onFooClick = function() {
    mainC.setActiveFoo(c.foo);
  
```

在上面的示例中，我们使用了一个调用父作用域函数的控制器函数。外部函数调用不是特定模板中的事件处理器。它可以包含在控制器中。这就是我们所做的。

我们需要对指令做的是添加表达式绑定：

```javascript
module.directive('foobar', function() {
  return {
    scope: true,
    controller: 'FoobarCtrl',
    controllerAs: 'c',
    bindToController: {
      onDelete: '&'
    },
    templateUrl: 'bar.html'
  };
});
```

一旦组件被使用，就会为新绑定接入表达式。如下所示：

```html
<foobar
  visible="mainC.isFooBarVisible()"
  language="mainC.getLanguage()"
  onDelete="mainC.deleteFoobar()">
</foobar>
```

该表达式绑定将从组件模板内部被调用。如下所示：

```html
<div ng-show="c.visible">
  <p>{{c.getText(c.language)}}</p>
  <button ng-click="c.onDelete()">
    Delete
  </button>
</div
```

## 结论

可以得出结论，AngularJS 是开发 Web 应用程序非常有用的框架。AngularJS 的用用体现在它对 HTML 所所的作用。通常，它是为了扩展 HTML 中包含的内容而开发的。注意，HTML 并不是为了 Web 应用程序而开发的。

然而，AngularJS 的出现填补了这一空白。

