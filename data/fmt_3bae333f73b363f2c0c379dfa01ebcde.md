
为了允许动态更改日期和时间的显示，你可能希望在代码中添加两个基本函数：

- 通用日期格式化函数。这将允许你传入一个日期对象和一个表示显示方式的字符串，并返回格式化后的日期。参见本章后面的示例代码了解如何实现。
- 通过设置设置特定的日期/时间例程。你应该在整个应用中调用一个通用函数来格式化日期时间。为了让这些例程尽可能快速，它们应该设置为针对所选日期/时间格式的优化例程。

# JavaScript • 优化原生 JavaScript

由用户。这将比每次需要格式化日期时间时运行条件逻辑更高效。你可以有一个在整个应用中调用的类似这样的通用例程：

```javascript
var formatDate = {};
```

然后你可以由每个用户指定其他函数。这将比每次需要格式化日期时间时运行条件逻辑更高效。你可以有一个在整个应用中调用的类似这样的通用例程。

# 每分钟更新日期的函数

```javascript
// 带有最新时间的全局对象
nowTime = {
  obj: new Date(),
  ms: 0,
  mins: 0,
  day: 0
}
var timerMinute = function(timerMinute) {
  clearTimeout(timerMinute);
  nowTime.obj = new Date();
  nowTime.ms = nowTime.obj.getTime();
  var mdate = nowTime.obj.getDate(); // 日期
  var newDay = (mdate != nowTime.day) ? true : false;
  nowTime.day = mdate;
  notifyListeners(nowTime, newDay);
  var nsecs = (60 - nowTime.obj.getSeconds()) * 1000;
  timerMinute = setTimeout(function() { timerMinute(); },nsecs);
}
timerMinute(); // 开始计时器
```

# 使用图标和颜色

你可以使用特殊图标来指示 OK、停止、警告或类似的情况。请注意，在美国有意义的图标（如停止标志或勾钩）在其他国家或文化中可能有不同的含义，或者没有含义。

颜色的使用也可能出现同样，例如红色和绿色、坏或好。你需要确保用法不会产生相反的含义，并且你有其他方式通过颜色表示意义。你还需要考虑你所选颜色对色盲用户是否可见。如果你依赖颜色来指示选择或强调，你可能希望包含一个选项部分，让用户可以选择他们喜好的组合。

# 日期和时间格式化函数

下面的代码是一个库例程，它可以根据你与要转换的字符串一起传递的“掩码”将日期和数字转换为显示字符串。函数被封装在一个对象 `xFormat` 中。对象顶部用于星期名称、月份名称以及小数点/逗号分隔符的数组和值应该被设置并更改，以反映当前的语言和国家偏好。

## 格式化日期：

```
var newstr = xFormat.formatDate(dateobj, mask);
```

```
obj =日期对象或 null，用于使用今天的日期
mask = 来自下方列表的字符字符串。任何未列出的字符
都将在格式化后的字符串中返回，例如 / 分隔符
示例："mm/dd/yy hh:nn am"
// nn: 分钟
// hh: 小时 (12小时制) HH: 小时 (24小时制)
// am: am 或 pm p (应用可以根据需要将其转换为大写)
// d: 月中的几 dd: 零填充 ddd: 周日
// m: 月份数字 mm: 零填充 mmm: 二月 mmmm: 二月
// yy: 年 yyyy: 2012
```

## 格式化数字

```
var n = xFormat.formatNumber(num, mask);
```

```
num = 需要格式化的数字
mask = 来自下方列表的字符字符串。在任何位置包含特殊
字符以在适当的位置显示该字符
示例:"$#,.##"
// $: 开头的美元符号
// R: 如果为负数，将数字变为红色
// G: 如果为正数，将数字变为绿色
// , 在千位之间加上逗号（你也可以使用 C）
// . 在小数点前加上点
// +- 在数字前加上加号或减号
// #: 代表数字，整个整数你只需要一个
使用小数点后的数字表示小数点的位数
// 在负数周围加上括号
// %: 数字末尾的百分比符号
```

## 示例函数

```
var xFormat = {
weekdayNames: ["Sunday", "Monday", "Tuesday", "Wednesday",
"Thursday", "Friday", "Saturday", "Sat"],
weekDayNames: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
monthNamesLong: ["January", "February", "March", "April", "May",
"June", "August", "September", "October", "November",
"December"],
monthNamesShort: ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul",
"Aug", "Sep", "Oct", "Nov", "Dec"],
strDec: ["", ", "],

formatDate: function(obj, mask) {
obj = (this.isDate(obj)) ? (obj) : (new Date(obj)):(new Date());
return this.formatTime(mask,
obj.getMinutes()),
};
```

```javascript
obj.getHours(),
obj.getDate(),
obj.getDay(),
obj.getMonth(),
obj.getUTCFullYear());
```

```javascript
isDate: function(obj) { 
  return Object.prototype.toString.call(obj) === '[object Date]';
}
```

```javascript
formatTimeDate: function(str, mins, hrs, mdate, wday, mon, yr) {
  var ampm = '';
  var hrzero = '';

  // 替换年份
  str = str.replace("yyyy",yr);
  str = str.replace("yy",(yr%100));

  // 替换月份日期
  var dayzero = (mdate < 10) ? "0" : "";
  str = str.replace("dddd", "xxxx");
  str = str.replace("ddd", "xxx");
  str = str.replace("dd", dayzero + date);
  str = str.replace("d", mdate);

  // 分钟
  var minszero = (mins < 10) ? "0" : "";
  str = str.replace("nn",minszero + mins);
  str = str.replace("n",mins);

  // 小时
  if (str.indexOf("H") >= 0) {
    hrzero = (hrs < 10) ? "0" : "";
    str = str.replace("HH",hrzero + hrs);
    str = str.replace("H",hrs);
  } else {
    ampm = "am";
    if (hrs >= 12) {
      hrs = (hrs > 12) ? (hrs-12) : hrs;
      ampm = "pm";
    }
    hrzero = (hrs < 10) ? "0" : "";
    str = str.replace("hh",hrzero + hrs);
    str = str.replace("h",hrs);
  }
}
```

# 126 • JavaScript: 优化原生 JavaScript

```javascript
// 12 小时制
str = str.replace("am","zz");
str = str.replace("a","z");
```

```javascript
// 月份（这样做是为了确保不会改变字符串中的任何 'am'）
var monzero = (mon < 9) ? "0" : "";
str = str.replace("mmmm","zzzz");
str = str.replace("mmmm"," "zzz");
str = str.replace("mm",monzero + (mon+1));
str = str.replace("m","m");
```

```javascript
// 替换临时占位符
str = str.replace("xxxx",this.weekdayNameLong[wday]);
str = str.replace("xxx",this.weekdayNameShort[wday]);
str = str.replace("zzzz",this.monthNamesLong[mon]);
str = str.replace("zzz",this.monthNamesShort[mon]);
str = str.replace("zz",ampm);
str = str.replace("z",ampm.substr(0,1));
return str;
```

```javascript
formatNumber: function (num) {
  if (typeof num != undefined && num != null) {
    var parts = num.toString().split(".");
    return parts[0].replace(/\B(\d{3})+(?=\d)/g, ",") + (parts[1] ? "." + parts[1] : "");
  } else {
    return "n/a";
  }
```

```javascript
// 格式化数字字符串 $, % - C
 mask 可以像这样：($+-,###%)
// 对于负数，除非添加会显示减号
formatNumberObj:function(str, mask) {
  str += '';
  var splitnum = mask.split('.');
  var numde = (splitnum.length < 2) ? 0 : splitnum[1].length - 1;
  var hasDollar = (mask.indexOf('$') >= 0);
  var hasPercent = (mask.indexOf('%') >= 0);
  var hasParen = (mask.indexOf('(') >= 0);
  var hasComma = (mask.indexOf(',') >= 0);
  var hasComma = (mask.indexOf('C') >= 0) ? true : hasComma;
  var hasPlus = (mask.indexOf('+') >= 0);
  var hasRed = (mask.indexOf('R') >= 0);
  var hasGreen = (mask.indexOf('G') >= 0);
}
```

```javascript
// 数字数字 - 小数点/逗号

var num = str.toString().replace(/,/g, ' ');

var num = +num;

if (isNaN(num)) return str;

var isNeg = (num < 0);

var isPos = (num > 0);

var num = Math.abs(num);

var num = num.toFixed(numde);

if (hasComma) num = this.formatNumber(num);

// 添加额外内容

var sfx = (hasPercent) ? ' %' : '';

sfx += (hasParen && isNeg) ? ')' : '';

if (isNeg) {

  var pfx = (hasParen) ? '(' : '-';

} else {

  var pfx = (hasPlus) ? '+' : '';

}

pfx += (hasDollar) ? '$' : '';

num = pfx + num + sfx;

if ((hasRed && isNeg) || (hasGreen && isPos)) {

  num = '<span style="color:' + (isNeg ? 'red' : 'green') + '">' + num + '</span>>';

}

return num;
```

# 语言本地化

如果你的应用程序将在其他国家发布，或被想要使用英语以外语言的用户使用，你需要在程序中添加相应的功能。步骤包括：

- 你需要确定支持哪些语言。然后你必须将所有的短语翻译成相应语言。有专业的服务可以为你完成此工作。
- 为一种语言创建一个文件，包含界面所需的所有语言字符串。
- 移除界面中硬编码的字符串，并将其替换为语言文件中相应的字符串。
- 在设置页面添加一个函数，允许用户选择界面语言。
- 添加一个在应用启动或用户在设置页面更改语言时调用的函数。这将调用任何需要动态更改显示字符串的视图处理器。

# 语言示例代码

以下代码是应用程序中处理语言本地化的一种方法示例。你可能也想查看现有的库。

- 1. 设置一些全局对象

```javascript
xLang = {};
xLang.uilang = {};
xLang.callbacks = {};
xLang.curLanguage = '';
xLang.language = {};
```

- 2. 加载你的 uilang['en'] = {

```javascript
vSETTINGS = {
