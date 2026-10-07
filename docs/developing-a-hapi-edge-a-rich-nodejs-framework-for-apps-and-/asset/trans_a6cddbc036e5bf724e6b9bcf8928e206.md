

编写一个 hapi 测试

测试耗时：6 ms
未检测到变量泄露

你在这里可以看到，在详细模式（verbose mode）下，你还可以看到每个测试的耗时。

## 编写一个 hapi 测试

hapi 在设计时就考虑了测试。为了发布版本，每一行代码和每一个代码路径都必须有相应的测试。因此，hapi 及其依赖项存在大量的测试。为了帮助缩短运行测试的时间，并避免文件描述符限制的问题，hapi 内置了对模拟请求（mock request）的支持。这是通过 `shot` 模块提供的名为 `inject` 的函数实现的。下面的测试用来说说明 `shot` 的威力。请注意，该测试没有使用实验性风格，而是使用 BDD 风格的测试快捷方式编写的。

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

Wreck 是一个轻量级的 HTTP/HTTPS 客户端封装，专为 hapi 设计。这是进行任何请求时首选的模块。尽管如此，`request` 模块也完全支持。在本地，`inject` 示例和 wreck 示例之间的测试时间差异约为 18ms。即使 18ms 本身并不多，你创建的所有测试累加起来很快。

## 代码覆盖率

除了 lab 中包含的所有功能外，代码覆盖（code coverage）是其最强大的特性之一。lab 的代码覆盖依赖于 `espree` 模块来生成 AST。对于典型的行覆盖，lab 还会确定不同的分支是否被测试执行。这可以是从 `if` 语句中的许多条件到标准的三元运算符的任何内容。此外，lab 还会确定某个代码路径是否应该执行以及是否可以被删除。
'html' 和 'console' 报告在显示代码覆盖方面测试得最充分。默认情况下，运行 lab 时不会启用代码覆盖。要启用它，你需要传递 `-c` 或 `--coverage` 标志。该标志将启用代码覆盖报告并确保测试覆盖了 100% 的代码。如果代码覆盖率低于 100%，可以使用 `-t` 或 `--threshold` 标志，后跟一个代表在报错前代码覆盖百分比的数字。如果测试未能通过阈值，lab 将带有错误代码退出。
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

Lab 包含了多种报告器：

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

如果你计划在 Jenkins 中使用 lab，junit 报告可能是一个很好的选择，因为许多 Jenkins 插件都依赖于这种格式，如 dashboard-view。你也可以结合 HTML 报告器和 HTML 发布插件来查看测试和代码覆盖的详细视图。json 报告器是一个非常易于解析的报告器，如果你需要查看原始数据进行自己的解析。它也会报告代码覆盖率以及通用测试。下面是使用 `-c` 标志启用 json 报告代码覆盖的输出示例：

```json
"17": {
  "source": "var data = [].concat(payload || '')",
  "chunks": [
    {
      "source": "var data = [].concat("
    },
    {
      "source": "payload",
      "miss": "true"
    },
    {
      "source": " | |"
    }
  ]
}
```

