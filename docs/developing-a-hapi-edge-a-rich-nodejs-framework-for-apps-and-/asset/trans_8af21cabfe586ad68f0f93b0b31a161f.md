

# 开发 hapi Edge

一个用于应用和服务的丰富 Node.js 框架

![](img/79450811086e2fc8749ec4d309ea2b79_0_0.png)

作者：Van Nguyen, Daniel Bretoi, Wyatt Preul, Lloyd Benson

前言：Eran Hammer

BLEEDING EDGE PRESS 出版

# 开发 hapi Edge

## 用于应用和服务的丰富 Node.js 框架

Van Nguyen, Daniel Bretoi, Wyatt Preul, Lloyd Benson

# 开发 hapi Edge

版权所有 (c) 2015 Bleeding Edge Press
保留所有权利。未经出版者书面许可，不得以任何形式或通过任何手段复制或传输本书的任何部分内容。

本书表达了作者的观点和意见。书中包含的信息提供时均不带任何明的、法定或暗示的保证。作者、Bleeding Edge Press 及其转销商或分销商均对因本书直接或间接引起或声称引起的任何损害不承担责任。

ISBN 9781939902207
出版商：Bleeding Edge Press, Santa Rosa, CA 95404
标题：Developing a hapi Edge
作者：Van Nguyen, Daniel Bretoi, Wyatt Preul, Lloyd Benson
编辑：Troy Mott
校对：Christina Rudloff
排版：Bob Herbstoff
网站：bleedingedgepress.com

# 目录

前言 | xi
序言 | xiii

第 1 章：hapi 简介 | 15
历史 | 15
书籍概述 | 16
hapi-plugins.com | 18
风格 | 18
总结 | 19

第 2 章：服务器 | 21
搭建一个简单的服务器 | 21
为 hapi-plugins.com 设置服务器 | 22
Glue | 26
Rejoice | 27
Confidence | 28
服务器方法 | 30
装饰服务器 | 31
缓存配置 | 31
请求生命周期 | 32
扩展点 | 34
总结 | 35

第 3 章：路由 | 37
路径处理 | 38
路由的组成部分 | 38
method (方法) | 39
vhost (虚拟主机) | 39
handler (处理器) | 39
config (配置) | 39
path (路径) | 41
服务器路由配置选项 | 43
总结 | 43

# 第 4 章：处理器 (handler) | 45
请求 | 45
parameters (参数) | 46
query (查询) | 46
payload (负载) | 47
headers (请求头) | 48
响应 (the reply) | 48
组织处理器 | 49
内置处理器 | 50
File (文件) | 50
proxy (代理) | 54
向处理器添加常用方法 | 55
绑定到服务器 | 55
装饰响应 | 56
Tails (尾部) | 56
使用 server.handler 定义处理器 | 57
点赞插件示例 | 58
上传文件 | 59
总结 | 60

# 第 5 章：验证 (Validation) | 61
验证的类型 | 61
Joi 验证 | 62
hapi-plugins.com 的验证 | 63
- 使用 joi 进行通用数据验证 | 65
使用验证函数 | 65
总结 | 66

# 第 6 章：插件 (Plugins) | 67
- 创建你自己的插件 | 68
插件配置 | 71
关于标签和选择插件的几点说明 | 73
何时使用插件 | 73
hapi 生态系统：一些常用插件 | 74
hapi-auth-basic | 74
blipp | 75
bell | 75
good | 75
tv | 75
lout / hapi-swagger | 75
poop | 76
更多插件 | 76
总结 | 76

# 第 7 章：身份验证 (Authentication) | 77
- 本章概述 | 77
方案 (Scheme) 与 策略 (strategy) | 77
hapi-auth-basic | 78
hapi-auth-cookie | 80
bell | 84
总结 | 86

# 第 8 章：模型 (Models) | 87
- 使用 HTTP | 87
预期用法 | 87
NPM 软件包 | 88
NPM 下载量 | 93
使用数据库 | 100
设置数据库 | 100
连接数据库 | 100
数据模型设计 | 101
总结 | 107

# 第 9 章：模板化 (Templating) | 109
配置 | 110
选项 | 111
视图加载 | 116
布局 (Layouts) | 116
配置 | 116
用法 | 117
排除 | 117
部分模板 (Partials) | 117
配置 | 117
辅助函数 (Helpers) | 118
配置 | 118
辅助文件 | 118
共享上下文 (Shared Contexts) | 119
总结 | 120

# 第 10 章：测试 (Testing) | 121
本章概述 | 121
lab 的历史 | 122
安装 lab | 123
安装 code | 124
编写一个简单的测试 | 124
lab 的原则 | 125
始终异步 | 125
测试脚本 | 127
安全全局变量 | 127
实验 | 128
编写 hapi 测试 | 129
代码覆盖率 | 131
报告器 (Reporters) | 133
代码检查 (Linting) | 136
插件测试 | 136
总结 | 138

# 第 11 章：调试 (Debugging) | 141
本章概述 | 141
console.log | 142
调试模式 (debug mode) | 142
TV | 143
Good | 144
REPL | 148
堆内存快照 (Heap Snapshots) | 148
核心文件 (Core Files) | 149
总结 | 151

# 第 12 章：安全 (Security) | 153
最佳实践 | 153
密码哈希 | 153
XSS | 154
CSRF | 155
SSL | 156
内容策略 | 157
CORS | 158
总结 | 159

# 第 13 章：附录 (Appendix) | 161
模型 | 163
历史 | 163
HTTP 客户端概述 | 163
数据库客户端概述 | 164
连接 | 167
- Sequelize | 170
- Mongoose | 171
- Cassandra | 172
- Apollo | 173
- 模板引擎概述 | 173

