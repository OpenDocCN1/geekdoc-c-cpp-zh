
```javascript
var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function (done) {
  Code.expect(lab).to.exist();
  done();
});
```

只需在项目根目录下输入命令 `lab` 即可运行上面的测试。输出将如下：

```
$ lab

1 tests complete

Test duration: 5 ms

No global variable leaks detected
```

希望这并不困难或令你感到惊讶。如你从输出中所看到的，运行测试的时间会连同点表示法的默认报告器一起报告出来。

# lab 的原则

让我们来看看需要记住的 `lab` 核心原则。

## 始终异步的

在上一节中，你看到了一个简单的 `lab` 测试是什么样子的。`lab` 的定义特征之一是测试始终被假设为异步的。并不是通过检查 `arguments` 对象的长度并对带有 `done` 参数的测试运行不同的逻辑，所有的 `lab` 测试必须接收一个回调参数，并在测试完成时执行它。如果测试没有期望某个参数，则测试将立即失败并给出解释。例如，下面的测试：

```javascript
// Load modules

var Code = require('code');
var Lab = require('lab');

var lab = exports.lab = Lab.script();

lab.test('lab exists', function () {
  Code.expect(lab).to.exist();
});
```

当我们运行 `lab` 时，得到以下输出：

```
$ lab
```

Error: Function for test "lab exists" should take one argument

同样，如果测试函数接受了参数但没有执行，将会发生错误。然而，这会导致测试超时。我们可以通过编写以下测试来观察这种超时：

```javascript
var Code = require('code');
var Lab = require('lab');
```

该测试的结果输出如下：

```
$ lab

Failed tests:

+ 1) exists

   Timed out (2000ms)
```

## 测试脚本

`lab` 的另一个假设是全局对象不应被变量污染。其他框架会将 `describe` 附加到全局对象上，而 `lab` 尝试了一种不同的隔离测试的方法。每个测试函数仅在 `script()` 返回的 `lab` 对象上可用。

## 安全全局变量

`Lab` 更进一步，在运行测试后会检查全局对象的属性。这通常是声明变量的迹象。然而，可以通过向二进制文件传递 `-l` 或 `--leaks` 来禁用此功能。同样，如果你有一个已知的全局变量，可以将其作为参数传递给 `-I` 或 `--ignore`。例如，如果你想忽略全局对象上名为 `foo` 的属性，你可以执行：

```
$ lab --ignore foo
```

## 实验 (Experiments)

虽然 `lab` 测试可以看起来像 `mocha` 和 `jasmine` 的 BDD 风格测试，但它们也可以完全命名。BDD 风格使用 `describe` 和 `it`，而 `lab` 也提供了 `experiment` 和 `test` 作为替代方案。`describe` 和 `experiment` 函数是互换的，就像 `it` 和 `test` 一样。你选择的风格完全取决于你，并没有标准答案。使用实验风格的一个优点是，它确实强化了工程师正在创建测试并且对它们进行某种科学尝试的概念。

实验有助于封装一组相似的测试。例如，如果你正在测试 `lab` 本身，你可以编写如下所示封装在实验中的实验测试。

```javascript
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

编写一个 hapi 测试

测试耗时：6 ms

未检测到变量泄露

你在这里可以看到，在详细模式（verbose mode）下，你还可以看到每个测试的耗时。

# 编写一个 hapi 测试

`hapi` 在设计时就考虑了测试。为了发布版本，每一行代码和每一个代码路径都必须有相应的测试。因此，`hapi` 及其依赖项存在大量的测试。为了帮助缩短运行测试的时间，并避免文件描述符限制的问题，`hapi` 内置了对模拟请求（mock request）的支持。这是通过 `shot` 模块提供的名为 `inject` 的函数实现的。下面的测试用来说说明 `shot` 的威力。请注意，该测试没有使用实验性风格，而是使用 BDD 风格的测试快捷方式编写的。

```javascript
// 加载模块
var Code = require('code');
var Hapi = require('hapi');
var Lab = require('lab');
```

```javascript
var lab = exports.lab.script();
var describe = lab.describe;
var it = lab.it;
var expect = Code.expect;
```

```javascript
describe('inject', function () {
  it('returns the response result', function (done) {
    var handler = function (request, reply) {
      return reply('hello');
    }

    var server = new Hapi.Server();
    server.connection();
    server.route({
      method: 'GET',
      path: '/',
      config: { handler: handler }
    });

    server.inject('/', function (res) {
      expect(res.statusCode).to.equal(200);
      expect(res.result).to.equal('hello');
      done();
    });
  });
});
```

在以前的示例中，`server.start` 函数没有被执行。结果是没有任何创建或挂载到服务器的 socket。然而，向服务器发送了请求并收到了响应。请求对象包含了服务器关心的所有属性。同样，传递给 `inject` 回调的响应对象包含了响应正文以及相关的响应头和状态码。

除非你正在从 socket 创建信息，否则最佳解决方案是使用 `inject`。如果你采用这种方法，测试的执行速度将比依赖真实 socket 快得多。此外，这使得更容易避免与 socket 相关的设置和清理工作。说到这里，如果你需要使用 socket，请向 `connection` 函数传递 0 作为端口，以确保端口被占用。注意，在服务器启动后可以从 `server.info.port` 属性获取实际使用的端口。

```javascript
// 加载模块

var Code = require('code');
var Hapi = require('hapi');
var Lab = require('lab');
var Wreck = require('wreck');
```

```javascript
var lab = exports.lab.script();
var describe = lab.describe;
var it = lab.it;
var expect = Code.expect;
```

```javascript
describe('real request', function () {

  it('returns a real response', function (done) {

    var handler = function (request, reply) {
      return reply('hello');
    }

    var server = new Hapi.Server();
    server.connection({ port: 0 });
    server.route({
      method: 'GET',
      path: '/',
      config: { handler: handler } };

    server.start(function () {
      Wreck.get('http://localhost:' + 
        server.info.port,
        function (err, res, payload) {
          expect(res.statusCode).to.equal(200);
          expect(payload).to.equal('hello');
          server.stop(done);
        }
      );
    });
  });
});
```

`Wreck` 是一个轻量级的 HTTP/HTTPS 客户端封装，专为 `hapi` 设计。这是进行任何请求时首选的模块。尽管如此，`request` 模块也完全支持。在本地，`inject` 示例和 wreck 示例之间的测试时间差异约为 18ms。即使 18ms 本身并不多，你创建的所有测试累加起来很快。

# 代码覆盖率

除了 `lab` 中包含的所有功能外，代码覆盖（code coverage）是其最强大的特性之一。`lab` 的代码覆盖依赖于 `espree` 模块来生成 AST。对于典型的行覆盖，`lab` 还会确定不同的分支是否被测试执行。这可以是从 `if` 语句中的许多条件到标准的三元运算符的任何内容。此外，`lab` 还会确定某个代码路径是否应该执行以及是否可以被删除。

'html' 和 'console' 报告在显示代码覆盖方面测试得最充分。默认情况下，运行 `lab` 时不会启用代码覆盖。要启用它，你需要传递 `-c` 或 `--coverage` 标志。该标志将启用代码覆盖报告并确保测试覆盖了 100% 的代码。如果代码覆盖率低于 100%，可以使用 `-t` 或 `--threshold` 标志，后跟一个代表在报错前代码覆盖百分比的数字。如果测试未能通过阈值，`lab` 将带有错误代码退出。

下面是 console 报告的输出，显示了未覆盖的样式。

```bash
$ lab -c
```

................................................................................

66 tests complete

Test duration: 1492 ms

未检测到全局变量泄露

Coverage: 99.44% (2/356)

lib/payload.js missing coverage on line(s): 17, 27

```

如果你没有检测到且希望对覆盖率有更好的概览，建议使用 'html' 报告。你可以使用不同的报告器，只需将报告器的名称传递给 `-r` 或 `--reporter` 标志即可。你可以看到运行 `lab -c -r html > coverage.html` 的输出截图。

```javascript

module.exports.Payload = function (payload, encoding) {

    Stream.Readable.call(this);

    var data = [].concat(payload || []);

    var size = 0;

    for (var i = 0, il = data.length; i < il; i++) {

        var chunk = data[i];

        size += chunk.length;

        data[i] = Buffer.isBuffer(chunk) ? chunk : new Buffer(chunk);

    }

    this._data = Buffer.concat(data, size);

    this._position = 0;

    this._encoding = encoding || 'utf8';

};

```

如你所示，仅在非常特定的变量中缺少了第 17 行和第 27 行的覆盖。然而，如果你为缺失的部分添加测试，就可以解决。

```bash

$ lab -c

```

................................................................................

69 tests complete
Test duration: 1492 ms
未检测到变量泄露
Coverage: 100%

% 报告器

使用覆盖率来开发模块是必须的。在代码覆盖部分，'console' 和 'html' 报告被展示了。然而，'html' 报告显示了每个测试的耗时。

`Lab` 包含了多种报告器：

- console - 命令行输出
- html - 输出到 HTML
- json - JSON 格式
- junit - JUnit 格式
- tap - TAP 格式
- lcov - lcov 格式
- clover - clover 格式
- custom - 自定义

## 测试报告 66 Failures (1450 ms)

| ID | Title | Duration (ms) |
|---|---|---|
| 1 | request() requests a resource | 21 |
| 2 | request() requests a POST resource | 6 |
| 3 | request() requests a POST resource with unicode characters | 5 |
| 4 | request() requests a POST resource with headers | 3 |
| 5 | request() requests a POST resource with stream | 5 |
| 6 | request() requests a resource without callback | 2 |
| 7 | request() cannot set an agent and rejectUnauthorized at the same time | 1 |
| 8 | request() cannot set a false agent and rejectUnauthorized at the same time | 0 |
| 9 | request() can set a null agent and rejectUnauthorized at the same time | 9 |
| 10 | request() requests an https resource | 345 |
| 11 | request() requests an https resource with secure protocol set | 297 |
| 12 | request() fails when an https resource has invalid cert and the default reject is false | 11 |
| 13 | request() succeeds when an https resource has unauthorized characters and rejectUnauthorized is false | 7 |
| 14 | request() requests a resource with downstream dependency | 6 |
| 15 | request() does not follow redirects by default | 3 |
| 16 | request() handles redirects | 4 |
| 17 | request() handles redirects with relative location | 5 |
| 18 | request() reaches max redirects count | 3 |

如果你计划在 Jenkins 中使用 `lab`，`junit` 报告可能是一个很好的选择，因为许多 Jenkins 插件都依赖于这种格式，如 dashboard-view。你也可以结合 HTML 报告器和 HTML 发布插件来查看测试和代码覆盖的详细视图。`json` 报告器是一个非常易于解析的报告器，如果你需要查看原始数据进行自己的解析。它也会报告代码覆盖率以及通用测试。下面是使用 `-c` 标志启用 json 报告代码覆盖的输出示例：

```json

"17": {

  "source": "var data = [].concat(payload || '')",
