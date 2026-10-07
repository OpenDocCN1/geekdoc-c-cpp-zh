

如你在上一个示例所示，当发生错误时，错误和堆栈跟踪会被记录到控制台，并带有 `Debug:` 前缀日志。

## TV

在开发过程中，调试 hapi 服务器的另一个有用选项是使用 `tv` 模块。`tv` 主要设计为 hapi 应用的前端消费者设计。其目标是提供一个易于使用的仪表板，显示服务器请求活动的信息。这对于前端开发者来说，能够追踪其代码向 hapi 服务器发送的请求的生命周期是特别用的。这里展示了 `tv` 的截图：

![](img/79450811086e2fc8749ec4d309ea2b79_142_0.png)

为了向服务器添加 `tv`，你像注册任何其他 hapi 插件一样注册它。下面显示了如何使用默认设置注册 `tv`。在服务器上注册 `tv` 后，你可以通过服务器 URL `/debug/console` 访问它。

```
var Hapi = require('hapi');
var Tv = require('tv');

var server = new Hapi.Server();
server.connection();

server.register(Tv, function (err) {

  if (!err) {
    server.start();
  }
});
```

通过这种方式，你可以通过选择不同的事件标签来订阅你关心的请求事件。请求详情会在它们产生时实时发送到 `tv` 页面。如果任何请求作为有用信息脱颖而出，你也可以对其进行星标并进行调查。

## 第 11 章：调试

## Good

在 `tv` 中记录请求详情对于本地开发是有用的。然而，当你处于 QA 或生产环境时，你将可能希望使用一个专门为该场景设计的模块。对于这些情况，以及本地开发，`good` 插件都是极其用的。

`good` 更加适用于 QA 和生产环境的原因是，它被设计为还可以记录操作数据。在多年来，它的功能已经扩展到不仅包含典型的内存或 CPU 详细信息，现在还包含了事件循环延迟和网络活动。
要向 hapi 服务器添加它，你像注册任何其他插件一样注册它。主要的区别在于，使用 `good` 时，你需要为你关心的事件类型以及记录这些事件的地方指定选项。`good` 事件包括以下内容：

- ops
- response
- log
- error
- request
- wreck

事件数据可以存储的地方非常广泛。如果你需要不同的报告器（reporter），可以通过查看许多示例之一构建一个。目前 `good` 可用的报告器包括以下类型：

- UDP
- HTTP
- Files
- Console
- InfluxDB
- Winston
- Loggly
- Logstash

这个列表将继续增长。你可以通过查看 `good` 页面获取最新列表。下面的代码显示了如何注册 `good` 并每秒将所有 `ops` 数据记录文件 `/var/log/example/ops.json`。

```
var Hapi = require('hapi');
var Good = require('good');
```

```
var server = new Hapi.Server();
server.connection();

var options = {
  opsInterval: 1000,
  reporters: {
    reporter: 'good-file',
    events: { ops: '+' },
    config: '/var/log/example/ops.json'
  }
};

server.register({
  register: Good,
  options: options,
}, function (err) {

  if (err) {
    console.error(err);
    return;
  }

  server.start();
});
```

当你查看 `ops` 日志文件时，你会发现每个条目都是 JSON 解析的，且每个条目都用换行符分隔。下面是事件数据的示例。

```
{
  "event": "ops",
  "timestamp": 1527940993174,
  "host": "mac.local",
  "pid": 35503,
  "os": {
    "load": [2.1342773475, 2.44287109375, 2.487046875],
  },
  "mem": {
    "total": 1717986184,
    "free": 5757075456,
    "uptime": 459461
  },
  "proc": {
    "uptime": 4,
    "mem": {
      "rss": 46538752,
      "heapTotal": 32171264,
      "heapUsed": 17638880
    }
  }
}
```

```
"delay": 0.2207310050725937,
"load": {
  "requests": {
    "concurrents": {"62778": 0},
    "responseTimes": {},
    "sockets": {
      "http": {
        "total":0
      },
      "https": {
        "total":0
      }
    }
  }
}
```

在在上的示例中，你可以看到记录了许多有用信息。这使得将比通常更高的内存占用与网络活动或事件循环缓慢关联成为可能。在版本 6 中，仍然支持使用 `wreck` 记录请求数据。这对于追踪你的 hapi 服务器和下游流之间可能存在的问题非常有用。
