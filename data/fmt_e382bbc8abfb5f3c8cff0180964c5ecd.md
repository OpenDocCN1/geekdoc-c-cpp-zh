
`"Settings"`, `"Search"`, `"Menu"`;

`MENU` = {};

`xLang.uilang['fr']` = {
  `vSETTINGS`: {
    `"Paramètres"`,
  }
}

```javascript
// - 3. 添加语言更改时调用的函数
xLang.changeLanguage = function(newlang) {
  if (newlang != xLang.curLanguage) {
    xLang.curLanguage = newlang;
    xLanguage = xLang.uilang[newlang];
    // 通知所有视图语言已更改
    for (var name in xLang.callbacks) {
      xLang.callbacks[name]();
    }
  }
};
```

```javascript
// - 4. 为每个显示 UI 字符串的视图添加回调函数
xLang.callbacks["settings"] = function () {
  document.getElementById("eTitle").innerHTML = xLanguage.vSETTINGS;
};
```

```javascript
// - 5. 初始化所有视图的默认语言
xLang.changeLanguage('en');
```

# 加载程序文件

有多种方法加载你的程序文件——构成应用程序的 HTML、CSS 和 JavaScript 文件。你决定的方法可能会取决于程序的通用用途以及你想要优化的变量。一些需要考虑的因素包括：

- 你可以在 HTML 中使用 `<script>` 标签来加载 JavaScript 文件。通常做法是将这些标签放在 HTML 的末尾，以便 UI 尽可能地加载和显示。大多数浏览器允许获取多个文件，但它们在加载和解析时会阻塞执行。加载较少、更大的文件有一个优势，但它们会阻塞更长时间。
- 你可能想要延迟加载某些不需要的文件，以提供更好的用户体验。你会在主 HTML 中包含脚本和样式标签，仅包含初始 UI 需要的代码。加载的 JavaScript 将包含按需要动态加载应用程序其余部分的代码。
- 你可能想要编程加载文件，以便根据用户设置或偏好加载不同的文件。你的初始脚本文件加载条件逻辑，使用配置值或 URL 中的信息来确定加载哪些文件。这对于你的应用程序支持不同品牌可能很有帮助。
- 你可能想要考虑使用类似 `require.js` 的加载器在需要时加载文件。这对于你的应用程序可能永远不需要某些文件很有帮助。
- 你应该考虑将你的文件合并，因为每次获取都有开销。你可以使用任何现有的压缩器或紧凑工具对每个文件进行压缩。使用压缩代码会使调试变得困难。使用仅删除了空格和注释的压缩代码，而不是更改变量和函数名称的混淆代码。由于 JavaScript 的弱类型和对 `eval` 的使用，混淆名称存在某些潜在危险。

# 使用文件加载器

我不倾向于使用 `require.js`，因为我通常希望在程序启动时按照我想要的顺序加载所有需要的文件，或者至少在显示第一个屏幕后加载。使用原生 JavaScript 运行时往往可以保持较小的代码体积。我通常有一个很小的 `index.html` 文件，它加载一个包含以下加载器代码的 `index.js` 文件。它从一个文件名数组中加载所有内容。

运行时 `true` `fact` 一个选项可以确保不返回缓存文件。如果变量 `cachebust` 被设置为 `true`，则会在每个请求的 URL 末尾添加随机字符串，以确保绕过任何缓存。`filesToLoad` 数组包含了你想要加载的所有文件的名称和类型。该数组可以写在文件中，也可以从配置文件加载。

如果需要，你还可以根据用户设置或运行时参数更改正在加载的文件的名称或位置。

## 1. 设置运行时以添加 DOM 元素

```javascript
//
if (window.addEventListener(function(type, attributes, innerHTML) {
  var attributes = attributes || {};
  var element = document.createElement(type);
  if (innerHTML) element.innerHTML = innerHTML;
  for (var key in attributes) {
    if (key == "class") {
      element.setAttribute("className", attributes[key]);
    } else if (key == "style") {
      element.style.cssText = attributes[key];
    } else {
      element.setAttribute(key, attributes[key]);
    }
  }
  return element;
});

// IE 除外
var createDOMElement = function(type, attributes, innerHTML) {
  attributes = attributes || {};
  var element = document.createElement(type);
  if (innerHTML) element.innerHTML = innerHTML;
  for (var key in attributes) {
    element.setAttribute(key, attributes[key]);
  }
  return element;
};
```

## 2. 决定是否要绕过缓存

```javascript
var cacheBust = true; // 设置为 true 以绕过缓存
```

## 3. 识别主 HTML 文件的 head 元素

```javascript
var xTag_Head = document.getElementsByTagName("head")[0];
```

## 4. 设置包含想要加载的文件详情的数组

```javascript
var filesToLoad = [];
filesToLoad.push({type:"js", url:"js/util.js"});
filesToLoad.push({type:"css", url:"css/main.css"});
filesToLoad.push({type:"html", url:"main.html"});
```

## 5. 设置你将调用的从数组加载所有文件的函数

```javascript
var loadFiles = function() {
  var nextobj = filesToLoad.shift();
  // 列表中的下一个文件
  if (nextobj) {
    loadFile(nextobj,loadFiles);
    // 全部完成
  } else {
    init(); // 启动程序的函数
  }
}
```

## 6. 设置准确加载文件的函数

```javascript
var loadFile = function(obj,callback) {
  var fileref;
  var newurl = obj.url;
  if (cacheBust) newurl += '?ts=' + (new Date()).getTime();
  // CSS
  if (obj.type == "css") {
    fileref=document.createElement("link");
    fileref.setAttribute("rel", "stylesheet");
    fileref.setAttribute("type", "text/css");
    fileref.setAttribute("href", newurl);
  }
  // CSS 文件不触发 onload - 设置定时器检查是否已加载
  var interval_id = setInterval(function() {
    try {
      if (fileref.sheet && fileref.sheet.cssRules.length) {
        clearInterval(interval_id);
        setTimeout(function() {if (callback) callback();},10);
      }
    } catch (e) {
    }
    xTag_Head.appendChild(fileref);
  },100);
  // JAVSCRIPT 文件
  else if (obj.type == "js") {
    fileref = document.createElement("script");
    fileref.setAttribute("type", "javascript");
    fileref.setAttribute("src", newurl);
    fileref.onload = function () {
      fileref.onload = fileref.onereadychange = null;
      if (xTag_Head && fileref.parentNode &&
      fileref.type==="text/javascript") xTag_Head.removeChild(fileref);
      setTimeout(function() {if (callback) callback();},10);
    }
    xTag_Head.appendChild(fileref);
  }
  // HTML 文件
  else if (obj.type == "html") {
    var req = new window.XMLHttpRequest;
    req.onereadychange = function() {
      if (req.readyState == 4 && (req.status == 0 ||
      req.status == 200)) {
        try {
          var dv2 = createElement("div",{id:obj.id,
          'class ':obj.sclass},req.responseText);
          document.getElementById(obj.element).appendChild(dv2);
        } catch (e) {
          console.log("ERROR LOADING "+newurl);
        }
        setTimeout(function() {if (callback) callback();},10);
      }
      req.open("GET", newurl, true);
      req.send("");
    }
  }
}
```

## 7. 现在，开始加载

```javascript
loadFiles();
```
