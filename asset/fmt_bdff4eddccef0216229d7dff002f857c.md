
```xml
<system.webServer>
<security>
  <requestFiltering allowHighBitCharacters="false" />
</security>
</system.webServer>
```

## 基于文件扩展名的过滤请求

文件扩展名过滤可以通过 `requestFiltering` 的 `fileExtensions` 部分以白名单或黑名单配置的方式工作。当配置为白名单时，只有匹配已配置的文件扩展名的请求才会被允许。当配置为黑名单时，发送到配置扩展名的请求将被拒绝。

默认情况下，请求过滤将停止对特定文件的请求，如 `.config`, `.asax`, `.cs` 和 `.vb` 文件。但如果您使用白名单来限制请求，那么您应该扩展默认黑名单过滤器以停止对 `.bak` 文件的请求。以下示例

```xml
<system.webServer>
<security>
  <requestFiltering>
    <fileExtensions allowUnlisted="true" >
```

```xml
<add fileExtension="*.bak" allowed="false"/>
<fileExtensions>
</requestFiltering>
</security>
<system.webServer>
```

## 基于请求大小过滤请求

通常，你并不拥有源代码的第三方组件可能会出现缓冲区溢出漏洞或对大请求产生其他不良反应。你可以使用 `RequestLimits` 元素以及 `maxAllowedContentLength`、`maxURL` 和 `maxQueryString` 属性，根据请求大小、URL 长度或 URL 中查询字符串的大小来配置请求过滤。

内容长度以字节为单位；URL 和查询字符串长度以字符为单位，如下：

```xml
<system.webServer>
  <security>
    <requestFiltering>
      <requestLimits 
        maxAllowedContentLength="300000000"
        maxUrl="260"
        maxQueryString="25"
      </requestLimits>
    </requestFiltering>
  </security>
</system.webServer>
```

## 基于 HTTP 动词过滤请求

在第 2 章中你学习了 GET 和 POST 动词。HTTP 规范在 HTTP 之上提供了其他动词和协议，开发者可以使用自己的动词。如果你确定你的应用程序不需要额外的动词，则可以使用 `verbs` 元素限制允许到达应用程序的动词，从而减少攻击面。类似于文件扩展名过滤，这可以在白名单或黑列表上工作。

以下代码段显示了如何限制到达应用程序的动词为 GET 和 POST：

```xml
<system.webServer>
  <security>
    <requestFiltering>
      <verbs allowedUnlisted="false" />
      <add verb="GET" allowed="true" />
      <add verb="POST" allowed="true" />
    </verbs>
    </requestFiltering>
  </security>
</system.webServer>
```

## 基于 URL 序列过滤请求

通常，第三方组件可能会根据 URL 序列出现问题，例如目录遍历攻击，该攻击通过在 URL 中引入 `../` 来尝试突破应用程序目录。可以使用 `denyUrlSequences` 部分配置请求过滤，根据 URL 中的序列停止请求。

例如，以下配置将拒绝任何包含 `..` 序列的请求：

```xml
<system.webServer>
  <security>
    <requestFiltering>
      <denyUrlSequences>
        <add sequence=".."/>
      </denyUrlSequences>
    </requestFiltering>
  </security>
</system.webServer>
```

## 基于请求段过滤请求

段过滤允许你拒绝尝试访问应用程序特定区域的 URL。默认情况下，IIS 使用段过滤拒绝所有尝试访问 `bin`、`App_code`、`App_GlobalResources`、`App_LocalResources`、`App_WebReferences`、`App_Data` 和 `AppBrowsers` 目录的请求。如果你有部分部分名称的“bin”和“binaries”，这比 URL 序列更灵活。使用 URL 过滤，你必须过滤 "bin"，这也会阻止对 "binaries" 的请求。

以下代码段将阻止访问 "bin" 段，但允许访问 "binaries" 段：

```xml
<system.webServer>
  <security>
    <requestFiltering>
      <hiddenSegments>
        <add segment="bin"/>
      </hiddenSegments>
    </requestFiltering>
  </security>
</system.webServer>
```

## 基于请求头过滤请求

最后，可以根据请求头的长度拒绝请求。结合请求大小和 URL 序列，这对于停止针对无法提供更新的第三方漏洞组件的攻击非常有用。你可以通过将标头添加到 `headerLimits` 部分来根据标头大小进行过滤，指定标头名称和最大字符数，如下：

```xml
<system.webServer>
  <security>
    <requestFiltering>
      <requestLimits>
        <headerLimits>
          <add header="Example" sizeLimit="2" />
        </headerLimits>
      </requestLimits>
    </requestFiltering>
  </security>
</system.webServer>
```

## 返回给拒绝请求的状态码

每个请求过滤规则都返回 404 状态并带有特定的子代码，允许你使用 IIS 日志监控工具监控日志性能。表 14.3 列出了每个角色返回的状态码。

表 14-3：请求过滤返回的状态码

| ERROR | 状态码 |
| :--- | :--- |
| URL 序列被拒绝 | 404.5 |
| 动词被拒绝 | 404.6 |
| 文件扩展名被拒绝 | 404.7 |
| 被隐藏段拒绝 | 404.8 |
| 因为请求头太大被拒绝 | 404.10 |
| 因为 URL 双重转义被拒绝 | 404.11 |
| 因为高位字符被拒绝 | 404.12 |
| 因为内容长度太大被拒绝 | 404.13 |
| 因为 URL 过长被拒绝 | 404.14 |
| 因为查询字符串过长被拒绝 | 404.15 |

## 使用日志解析器挖掘 IIS 日志文件

IIS 日志文件是关于 Web 应用程序活动的有用信息源，可以主动用于（例如，监控日志文件中的可疑活动）和响应地（例如，排查应用程序出现的问题）。

## 使用 Log Parser 挖掘日志文件

IIS 日志文件是关于 Web 应用程序活动的有用信息源，可以主动用于（例如，监控日志文件中的可疑活动）和响应地（例如，排查应用程序出现的问题）。

### 表 14-4：可用的 IIS 日志选项

| 名称 | 说明 |
| :--- | :--- |
| date | 相关性日期 |
| time | 相关性时间 |
| c-ip | 客户端 IP 地址 |
| cs-username | 用户名 |
| s-servername | 服务名称 |
| s-computername | 服务器名称 |
| s-ip | 服务器 IP 地址 |
| s-port | 服务器端口 |

### 表 14-4（续）

| 名称 | 说明 |
| :--- | :--- |
| cs-method | 有助于识别 POST 请求 |
| cs-uri-stem | 识别访问的页面 |
| cs-uri-query | 识别请求中的查询 |
| sc-status | 记录返回给客户端的 HTTP 状态 |
| sc-substatus | 记录返回给客户端的 HTTP 子状态 |
| sc-win32-status | Win32 状态 |
| cs-bytes | 发送字节数 |
| cs-bytes | 接收字节数 |
| time-taken | 耗用时间 |
| cs-version | 协议版本 |
| cs-host | 包含请求中的主机名 |
| cs (User-Agent) | 用户代理 |
| cs (Cookie) | Cookie |
| cs (Referer) | 引用页 |

# 使用 Log Parser 挖掘 IIS 日志文件 | 37

在对日志文件运行任何数据之前，你应该先对其进行备份，并在副本上运行挖掘操作。在网站被黑客入侵的情况下，你可能需要证据，只有当日志文件是真实且未被变动过时才能使用。复制文件还有另一个优势：你可以通过只复制你认为攻击发生的时间段的文件，来减少需要查找的数据量。

在潜在攻击发生后，你想要运行的第一个查询是你的网站上托管资源的访问次数。单个资源的高请求数可能表明该资源正受到攻击。以下命令行使用 `LogParser` 解析并显示任何 `*.aspx` 页面和 Windows 通信框架 (WCF) 服务（以 `.svc` 结尾的文件）：

```
LogParser SELECT TOP 10 cs-uri-stem as url,COUNT(cs-uri-stem) as hits
FROM ex* WHERE cs-status=400 OR cs-status =500 AND
(TO_LOWERCASE(cs-uri-stem) LIKE '*.aspx*')
OR TO_LOWERCASE(cs-uri-stem)
LIKE '*.svc*') GROUP BY url ORDER BY hits DESC
```

当针对我为了测试目的托管在服务器上的 Graffiti 实例日志运行此查询时，返回的数据大致如下所示。你会发现一些对于博客服务器来说是不寻常的：评论页面、首页以及单个条目（这些加载最频繁的页面）。

| url | hits |
|---|---|
| /CommentView.aspx | 5885 |
| /Default.aspx | 3051 |
| /Default.aspx.n/CommentView.guid,3dedal1a-74e6-49e9-af3d-09d27d15b19e.aspx | 870 |
| /FormatPage.aspx | 803 |
| /Trackback.aspx | 711 |
| /2006/09/03/TestTitlePostUsingWindowsLiveWriterBeta.aspx | 602 |
| /Login.aspx | 535 |
| /Archives.aspx | 448 |
| /feed/Default.aspx | 405 |

```
Statistics:
-------
Elements processed: 62143
Elements output: 10
Execution time: 1.98 seconds
```

让我们仔细观察此查询，以展示 Log Parser 如何工作。表 14-5 显示了所用 SQL 查询各部分的详细说明。

## 表 14-5：Log Parser 查询部分分解

| QUERY PART | PURPOSE |
| --- | --- |
| SELECT TOP 10 cs-uri-stem AS url, COUNT(cs-uri-stem) AS hits | 选择 cs-uri-stem 列，将其重命名为 url，并通过统计其在已处理的日志文件中出现的总数来选择其访问次数。将列命名为 hits。TOP 10 限制指示 Log Parser 仅返回找到的前十个结果。 |
| FROM ex*.log | 选择要使用的数据源——在这种情况下，是任何以 ex 开头并具有 .log 扩展的文件。 |
| WHERE (sc-status<400) OR (sc-status>=500) | 限制处理的记录，排除任何返回状态码在 400 到 500 之间的请求。HTTP 规范规定这些状态码表示明显的错误，例如请求不存在的响应。 |
| AND (TO LOWERCASE(cs-uri-stem) LIKE '%.as%' OR LOWERCASE(cs-uri-stem) LIKE '%.svc') | 限制处理的记录为包含 .as%（其中 .as 是通配符）或 .svc 的 URL，从而将查询限制在默认的 ASP NET 页面扩展上。 |
| GROUP BY url ORDER DESC | 按 URL 对结果进行分组，然后按访问次数降序排列结果，将最流行的请求放在结果顶部。 |

你可以通过以下查询将解析使用细分为每日访问次数：

```
LogParser "SELECT TO_STRING(TO_TIMESTAMP(date, time),
'yyyy-mm-dd') AS day,
cs-uri-stem AS url, COUNT(cs-uri-stem) AS hits FROM ex*.log WHERE
(sc-status<400 OR sc-status>=500) AND
(TOLOWERCASE(cs-uri-stem) LIKE '%.as%'
OR LOWERCASE(cs-uri-stem) LIKE '%.svc') GROUP BY day,
ORDER BY day DESC" -rtp:1
```

特定资源访问次数较多可能指示潜在攻击。另一个指标是每小时内的错误数量。比正常高的错误数量可能表明攻击者正在对你的应用程序进行扫描。以下查询返回任何错误数量超过 50 个的小时，你显然需要调整速率限制（rate limit）以匹配你的网站。

```
LogParser *SELECT date, QUANTIZE(time, 3600) AS hour, sc-status
Count(*)
AS Errors FROM ex*.log WHERE sc-status =400
GROUP BY date, hour, sc-status
HAVING Errors>50 ORDER BY Errors -rtp:1
```

当针对示例日志执行此查询时，返回了以下结果，这可能表明在 2008 年 12 月 13 日 16:00 到 17:00 之间对服务器进行了操作：

| date | hour | sc-status | |
|---|---|---|---|
| 2005-08-09 | 04:00 | 404 | 57 |
| 2008-12-20 | 17:00 | 404 | 54 |
| 2005-08-09 | 03:00 | 404 | 68 |
| 2009-05-21 | 08:00 | 404 | 52 |
| 2005-08-10 | 05:00 | 404 | 51 |
| 2008-12-13 | 18:00 | 404 | 128 |

```
Statistics:
Elements processed: 62143
Elements output: 6
Execution time: 1.82 seconds
```

状态码为 404 的错误并不是问题。但同一 IP 地址的大量 404 错误结合 200（成功）状态码可能表明攻击成功了。以下查询检查 2008 年 12 月 13 日的日志文件，并提取出既导致了 404 又成功加载页面的 IP 地址：

```
LogParser *SELECT c-ip, cs-uri-stem, Count(*)
as HITS FROM ex*.log WHERE
TOLOWERCASE(cs-uri-stem) NOT LIKE '%.css' AND
TOLOWERCASE(cs-uri-stem) NOT LIKE '%.jpg' AND
TOLOWERCASE(cs-uri-stem) NOT LIKE '%.png' AND
TOLOWERCASE(cs-uri-stem) NOT LIKE '%.gif' AND
c-ip IN (SELECT c-ip FROM ex081213.log WHERE sc-status=404) AND
sc-status=200 GROUP BY c-ip, cs-uri-stem ORDER BY hits -rtp:-1
```

结果显示没什么担心：

| c-ip | cs-uri-stem | Hits |
|---|---|---|
| 69.147.90.42 | /error.htm | 94 |
| 81.174.237.97 | /WebResource.axd | 62 |
| 69.147.90.42 | /SyndicationService.asmx/GetAtom | 46 |
| 81.174.237.97 | /graffiti-admin/ajax.ashx | 44 |
| 81.174.237.97 | /graffiti-admin/reporting/charts.ashx | 32 |

## 第 14 章保护互联网信息服务器 (IIS)

结果顶部的 IP 地址属于雅虎；另一个 IP 地址是我自己的。如果你想查看某个特定 IP 地址发送了什么浏览器标识符，可以使用以下查询：
