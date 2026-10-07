
接下来，你可以看到我们实现相同功能的代码示例。注意，`true` 和 `exist` 在代码中是函数。

```
expect(foo).to.exist();
expect(bar).to.be.true();
```

除了前面描述的不一致性外，我们还想要一个轻量、简单且直观的断言库。lab 删除了处理插件、扩展以及支持浏览器测试的开销部分。这包含了我们大部分所需的功能，但代码量只有约 300 行，易于阅读和理解。

最后，`code` 允许测试运行器与断言库之间进行深度集成。这使得我们能够获取总断言数来衡量测试的全面，并验证每个生成的断言确实已执行。

Lab 也有其他方式。例如，增加了对编译器的支持以支持 CoffeeScript 或 JSX 代码。此外，lab 现在内置了支持，使得对 hapi 的请求遵循相同的编码风格。这有助于开发者在请求合并代码之前提前知道自己是否违反了任何样式规则。然而，lab 的缺点之一是它目前仅设计并运行在服务器端。不过，随着其流行程度增加和越来越多的开发者希望用它进行客户端测试，这一点可能会发生变化。

## 安装 lab

lab 可能在你的环境中全局安装很有有用。与其他 node.js 模块类似，可以使用 `npm` 安装 lab。如下所示。

```
$ npm install -g lab
```

虽然你可以全局安装 lab，但没有必要这样做。相反，所有的 hapi 核心模块都在其 `package.json` 的 `devDependencies` 部分中包含了 lab。任何最近版本的 lab 都可以全局或本地安装，因为它们在运行测试时不会发生冲突。接下来的示例显示了如何仅在本地安装 lab 并将其保存到 `package.json` 的 `devDependencies` 部分。

```
$ npm install lab --save-dev
```

安装 lab 之后，你应该验证它运行是否正常。如果是全局安装的，lab 将在 `PATH` 环境变量中可用。否则，你需要从 `node_modules/.bin` 文件夹运行 lab 二进制文件。要验证全局安装的 lab，只需运行 `lab -h`。如果你想验证本地安装，则需要运行 `node ./node_modules/.bin/lab -h`。你应该能得到 lab 的帮助页面。

顺便提一下，当进入带有子目录 `node_modules/.bin` 的文件夹时，自动更新 `PATH` 可能会有帮助。这会让本地二进制文件的运行方式与全局二进制文件相同。

## 安装 code

与安装 lab 的方式类似，你也应该安装 `code`。记住，lab 并没有内置开箱即用的断言库。因此，你应该使用 `code`、`chai` 或任何你喜欢的其他模块。你可以再次运行 `npm install code --save-dev` 将其保存到 `package.json` 文件中，或手动添加。

## 编写示例测试

所有测试应该位于项目根目录下的 `test` 文件夹中。这种模式在 Node.js 社区中几乎无处不在。如何命名你的测试文件取决于你，目前并没有一个统一的命名规范。然而，hapi 组织中所有模块使用的一种模式是将每个测试文件命名为与它负责测试的对应模块同名。为了这次练习，在 `test` 文件夹中创建一个名为 `index.js` 文件。用以下代码填充 `index.js`。

```
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function (done) {
  Code.expect(lab).to.exist();
  done();
});
```

只需在项目根目录下输入命令 `lab` 即可运行上面的测试。输出将如下：

$ lab

1 tests complete
Test duration: 5 ms
No global variable leaks detected

希望这并不困难或令你感到惊讶。如你从输出中所看到的，运行测试的时间会连同点表示法的默认报告器一起报告出来。

## lab 的原则

让我们来看看需要记住的 lab 核心原则。

### 始终异步的

在上一节中，你看到了一个简单的 lab 测试是什么样子的。lab 的定义特征之一是测试始终被假设为异步的。并不是通过检查 `arguments` 对象的长度并对带有 `done` 参数的测试运行不同的逻辑，所有的 lab 测试必须接收一个回调参数，并在测试完成时执行它。如果测试没有期望某个参数，则测试将立即失败并给出解释。例如，下面的测试：

```
// Load modules

var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function () {
  Code.expect(lab).to.exist();
});
```

当我们运行 lab 时，得到以下输出：

```
$ lab
```

Error: Function for test "lab exists" should take one argument

同样，如果测试函数接受了参数但没有执行，将会发生错误。然而，这会导致测试超时。我们可以通过编写以下测试来观察这种超时：

```
var Code = require('code');
var Lab = require('lab');
```

该测试的结果输出如下：

$ lab

Failed tests:
+ 1) exists
   Timed out (2000ms)

### 测试脚本

lab 的另一个假设是全局对象不应被变量污染。其他框架会将 `describe` 附加到全局对象上，而 lab 尝试了一种不同的隔离测试的方法。每个测试函数仅在 `script()` 返回的 lab 对象上可用。

### 安全全局变量

Lab 更进一步，在运行测试后会检查全局对象的属性。这通常是声明变量的迹象。然而，可以通过向二进制文件传递 `-l` 或 `--leaks` 来禁用此功能。同样，如果你有一个已知的全局变量，可以将其作为参数传递给 `-I` 或 `--ignore`。例如，如果你想忽略全局对象上名为 `foo` 的属性，你可以执行：

```
$ lab --ignore foo
```

### 实验 (Experiments)

虽然 lab 测试可以看起来像 mocha 和 jasmine 的 BDD 风格测试，但它们也可以完全命名。BDD 风格使用 `describe` 和 `it`，而 lab 也提供了 `experiment` 和 `test` 作为替代方案。`describe` 和 `experiment` 函数是互换的，就像 `it` 和 `test` 一样。你选择的风格完全取决于你，并没有标准答案。使用实验风格的一个优点是，它确实强化了工程师正在创建测试并且对它们进行某种科学尝试的概念。

实验有助于封装一组相似的测试。例如，如果你正在测试 lab 本身，你可以编写如下所示封装在实验中的实验测试。

```
// Load modules
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();
lab.experiment('lab', function () {
  lab.test('exists', function (done) {
    Code.expect(lab).to.exist();
    done();
  });
lab.test('has properties', function (done) {
    Code.expect(Object.keys(lab)).to.not.have.length(0);
    done();
  });
});
```

然后如果你以详细模式运行这些测试，你将得到：

```
$ lab -v
lab
1) exists (3 ms)
2) has properties (1 ms)
```
