

## 创建参考复选框和检查清单的标记。

下载 form/checklist/index_for_book.html

```html
<table id="mailbox">
  <thead>
    <tr>
      <th><input type="checkbox" id="toggler" /></th>
      <th>Subject</th>
      <th>Date</th>
      <!-- From, Size, Attachments... -->
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><input type="checkbox" name="mail_ids[]" value="1" /></td>
      <td>Happy new year!</td>
      <td>Jan 1, 2010 00:03am</td>
      <!-- ... -->
    </tr>
    <!-- More rows... -->
  </tbody>
</table>
```

## 将选中状态传播到每行的第一个复选框。

下载 form/checklist/checklist.js

```javascript
function toggleAllCheckboxes() {
  var scope = this.up('table').down('tbody'), boxes = scope && scope.select('tr input[type="checkbox"]:first-of-type');
  var refChecked = this.checked;
  (boxes || []).each(function(box) { box.checked = refChecked; });
}

document.observe('dom:loaded', function() {
  $('toggler').observe('click', toggleAllCheckboxes);
});
```

## 21 验证表单：基础

客户端验证是必备的。说真的。无论你的用户连接吞吐量如何，如果本可以在浏览器中直接完成的验证还非得在服务器上来回往返一趟，那简直令人痛心。你当然希望自己的网页只带来骄傲，所以让我们开始吧！

第一个任务专注于最基本的验证类型：必填字段，即验证特定字段是否有非空文本或是否被勾选等等。我们将使用一种约定：用 `required` CSS 类标记这些字段，并依靠样式来对缺失字段提供视觉反馈。

首先，务必拦截表单的 submit 事件，而不是提交按钮的 click 事件或文本框的 Return 键。要在表单提交到服务器之前对其进行拦截，唯一可靠的方式就是它的 submit 事件。即使是程序化提交（`form.submit()` 调用）也会触发该事件。

一旦挂钩，我们只需要获取表单中所有标记为 required 的元素，并验证它们具有非空值。Prototype 对 String 的 `blank()` 扩展在这里很方便。仅包含空白字符的字符串被视为空白，从语义角度来看，它们肯定不比真正的空字符串好多少。但请注意，如果某个字段允许只含空白，那么你可以直接使用 `if (field.getValue())`——在 JavaScript 中，空字符串等价于 false。

我们的代码维护一个 `firstOffender` 引用，以便通过自动聚焦第一个有问题的字段来帮助用户更正输入。最后但同样重要的是，一旦我们完成检查，如果至少有一个问题，我们就 `stop()` 该事件，从而有效地阻止当前表单被提交。

最后提醒：默认情况下，submit 事件在 Internet Explorer 中不会冒泡。因此，如果你的代码也需要在 IE 中运行，就必须为页面上要检查的每个表单都附加事件监听器，包括在初始 DOM 加载后动态插入的表单。jQuery 从 1.4 版本起在 IE 中模拟了 submit 事件的冒泡，但代价是对表单内的所有点击和按键进行相当繁重的监控。

### 标记必填字段。

```html
<form id="registration">
<p>
<label for="user_first_name">First name</label>
<input type="text" name="user[first_name]" id="user_first_name" class="required text" />
</p>
<!-- ...more fields... -->
<p class="radios">
<input type="checkbox" id="terms" name="terms" class="required" />
<label for="terms">I accept the terms of service*</label>
</p>
<p><input type="submit" value="Sign me up! " /></p>
</form>
```

### 检测缺失的必填字段。

```javascript
function checkForm(e) {
  var firstOffender, value;
  this.select('.required').each(function(field) {
    value = field.getValue();
    if (value && !value.blank()) {
      field.up('p').removeClassName('missing');
    } else {
      firstOffender = firstOffender || field;
      field.up('p').addClassName('missing');
    }
  });
  if (firstOffender) { e.stop(); firstOffender.focus(); }
}
document.observe('dom:loaded', function() {
  $('registration').observe('submit', checkForm);
});
```

### 相关任务

- 任务 22，*进一步验证表单*，在下一页
- 任务 23，*验证表单：全套验证*，在第 68 页

## 22 验证表单：更进一步

之前的任务让我们检查必填字段是否确实已填写或勾选。很好。然而，我们经常希望文本字段符合给定的格式，例如电话号码、电子邮件地址、整数或更一般的数字。这些字段可能已填写但不正确，我们应该尽最大努力提前检查。一如既往，这只是对真正强制性检查（即服务器端检查）的*补充*。

通常的做法是使用正则表达式，这种方式相当简洁高效。如果你在开发者生涯的现阶段还不太熟悉正则表达式，请帮自己一个大忙，花几个小时深入研究一下。虽然它们在初学者看来可能难以理解，但它们建立在极少数语法规则之上（大约十几条，其中一半通常就够用了），了解“正则表达式”将无数次为你节省大量编码时间。你可以在网上找到大量优秀的交互式教程。

在对面页上，代码的思路是检测与基于正则表达式的检查相匹配的表单字段上的 CSS 类。我只放了三个正则表达式，但你可以通过向 `FIELD_PATTERNS` 字典添加新的键值对来扩展功能。不过，让我先打消纯粹主义者的不满。是的，我展示的模式并没有涵盖非十进制数字、指数浮点记数法，以及当今使用的约 0.1% 的电子邮件地址。这有什么大不了的。但本任务讲的是字段验证，而不是正则表达式功夫。你可以随意调整这些模式以满足你的需求！

这段代码相当简短直接；这里我只想说明两个有趣的点。首先，`$F(element)` 函数只是 `element.getValue()` 的简写符号。

其次，如果你在 JavaScript 中使用过正则表达式，大概率你会使用通用的 `myString.match(myPattern)` 方式。这可行，因为它返回 null（无匹配）或匹配数组（或匹配组）。然而，当你只需要知道是否找到匹配，而不关心匹配的具体内容时，你应该反转问题，让模式对字符串调用 `test()`，它只返回一个布尔值。

事实上，`test()` 方法更健壮：如果传入的不是字符串，它不会出错；而试图在非字符串上调用 `match()` 则会失败。另外，`test()` 的效率略高一些。我喜欢理所当然地使用这类性能优化手段，尤其是在它们不会带来代码可读性（或代码体积）损失的情况下。

### 标记需要特殊语法的字段。

```html
<p>
  <label for="user_email">Email</label>
  <input type="text" name="user[email]" id="user_email"
    class="required text email" />
</p>
<p>
  <label for="user_favnumber">Favorite number</label>
  <input type="text" name="user[favnumber]" id="user_favnumber"
    class="text number" />
</p>
```

### 检查特殊语法的字段。

```javascript
var FIELD_PATTERNS = {
  integer: /^\d+$/,
  number: /^\d+(?:\.\d+)?$/,
  email: /^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,6}$/i
};

function checkField(field) {
  var value = $F(field).toString().strip();
  for (var pattern in FIELD_PATTERNS) {
    if (!field.hasClassName(pattern)) continue;
    if (!FIELD_PATTERNS[pattern].test(value)) return false;
  }
  return true;
}
```

### 相关任务

- 任务 21，*验证表单：基础*，在第 64 页
- 任务 23，*验证表单：全套验证*，在下一页

## 23 验证表单：全套验证

### 标记登录字段。

下载 form/validation_ajax/index.html

```html
<p>
  <label for="user_login">Login</label>
  <input type="text" name="user[login]" id="user_login" class="required text" />
  <span class="feedback" style="display: none;"></span>
  <img src="spinner.gif" class="spinner" style="display: none;" />
</p>
```

### 监听登录字段。

下载 form/validation_ajax/validation_ajax.js

```javascript
document.observe('dom:loaded', function checkLogin() {
  var feedback = $('user_login').next('.feedback'),
      spinner = $('user_login').next('.spinner');
  new Field.Observer('user_login', 0.8, function(_, value) {
    if (value.length < 2) return;
    feedback.hide(); spinner.show();
    new Ajax.Request('check_login.php', {
      method: 'get', parameters: { login: value },
      onComplete: function(res) {
        if (Ajax.activeRequestCount > 1) return;
        if (res.request.success && res.status) {
          feedback.update('Login available!').removeClassName('ko');
        } else {
          feedback.update('Login taken!').addClassName('ko');
        }
        spinner.hide(); feedback.show();
      }
    });
  });
});
```

### 模拟登录检查。

下载 form/validation_ajax/check_login.php

```php
<?php
sleep(rand(5, 10) / 10.0); // Simulate intarwebs delay...
$RESERVED = array('bob', 'doudou', 'tdd', 'meshak', 'ook');
$login = isset($_GET['login']) ? $_GET['login'] : '';
$response = in_array($login, $RESERVED) ? '422 Conflict' : '202 Accepted';
header('HTTP/1.1 ' . $response);
?>
```

