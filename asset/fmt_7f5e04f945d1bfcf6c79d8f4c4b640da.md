
```json
  "userPassword": "178593454@",

  "userEmail": "mudassarali.official@gmail.com",

  "createdAt": "2021-04-16T20:41:15.432Z",

  "isDeleted": false

}
```

# 使用 Swagger 进行 API 测试

数据成功提交后，你可以看到我们的服务器响应为 `true`，这表明我们的数据已成功提交到数据库。

![](img/ecf1b6d3def03c95166d6223c24cb862_124_0.png)

![](img/ecf1b6d3def03c95166d6223c24cb862_124_1.png)

125

![](img/ecf1b6d3def03c95166d6223c24cb862_125_0.png)

## 总结

`Swagger` (`Open API`) 是一种用于描述和记录 REST API 的与语言无关的规范。它允许机器和开发者在无需直接访问项目源代码的情况下理解机器的工作原理和功能。`Swagger` (`Open API`) 的主要目标是尽量减少连接微服务的工作量。`Swagger` 配合开源工具集使用，用于设计、构建和使用 Restful Web 服务。`Swagger` 包含了自动化文档代码生成。`Swashbuckle` 的三个主要组件：

- `Swashbuckle.AspNetCore` 是用于暴露 `Swagger` 的中间件
- `Swashbuckle.AspNetCore.SwaggerGen` 从你的控制器和模型构建 `Swagger` 对象，此包与 `Swagger` 中间件结合以自动暴露 `Swagger`
- `Swashbuckle.AspNetCore.UI` 是 `Swagger UI` 的嵌入版本，通过解释 `Swagger` 来构建一个高度可定制的实用工具，用于解释 Web 功能。

## 结论

现在关于 Open Swagger，它是记录 Restful API 的最佳 Open API。作为一名开发者，我在使用 `Swagger` 测试 restful API 方面有丰富的经验，可以发送完整对象并以高效的方式获取响应。在完成 `.NET Core` 配置后，可以享受 `Swagger` 的便利。

# 在 Azure 上部署应用

- 概述
- 介绍
- 部署步骤
- 结论

`App Service` 让你快速构建、部署和扩展企业级 Web、移动应用，并在完全托管的平台上运行，满足性能、可扩展性和合规性要求。

## 打开 Azure 门户

首先你需要打开 Azure 账户，然后选择你想部署应用的 Azure 订阅。区域对于应用的部署成本非常重要，所以我选择了“美国中部”（Central US）。

![](img/ecf1b6d3def03c95166d6223c24cb862_128_0.png)

## 创建 Azure 资源组

现在选择 Azure 订阅并创建 Azure 资源组。

![](img/ecf1b6d3def03c95166d6223c24cb862_129_0.png)

## 选择应用名称

选择应用名称，我的 Web 名称是 -Api

![](img/ecf1b6d3def03c95166d6223c24cb862_129_1.png)

## 选择运行时栈

在选择名称和资源组后，为你的应用选择运行时，我的应用使用的是 Microsoft Azure `.NET 6` 最新稳定版本。

![](img/ecf1b6d3def03c95166d6223c24cb862_130_0.png)

## 创建 App Service Plan

`App Service Plan` 定义了运行 Web 应用的一组计算资源。这些计算资源类似于传统托管中的服务器场。一个或多个应用可以部署在相同的计算资源（同一个 `App Service Plan`）上。

## 选择定价计划

现在选择层级 Dev/Test、Production、Isolated。

## 现在我们的应用开发和测试目的是我们选择了 Dev/Test

## 选择部署选项

启用 `GitHub Actions` 以持续部署您的应用。`GitHub Actions` 是一个自动化框架，每当存储库中进行新提交时，它可以构建、测试并部署您的应用。如果您的代码在 GitHub 上，请在此处选择您的存储库，我们将添加工作流文件以自动将您的应用部署到 `App Service`。如果您的代码不在 GitHub 上，请在创建 Web 应用后转到部署中心来设置部署。

![](img/ecf1b6d3def03c95166d6223c24cb862_133_0.png)

## 选择网络选项

配置 Web Apps 时，其入站地址可以对互联网公开，也可以被隔离在 Azure 虚拟网络中。Web Apps 还可以配置出站流量以访问虚拟网络中的端点，这些流量受网络安全组管理或受虚拟网络路由的影响。默认情况下，您的应用对互联网开放，且无法访问虚拟网络。这些方面在应用配置后也可以进行更改。

## 选择 Azure 监控选项

`Azure Monitor Application Insights` 是一种为开发者和 DevOps 专业人员提供的应用程序性能管理 (`APM`) 服务。在下方启用它以自动监控您的应用程序。它将检测性能异常，并包含强大的分析工具，帮助您诊断问题并理解用户实际上对您的应用做了什么。

![](img/ecf1b6d3def03c95166d6223c24cb862_134_0.png)

![](img/ecf1b6d3def03c95166d6223c24cb862_134_1.png)

![](img/ecf1b6d3def03c95166d6223c24cb862_134_2.png)

## 选择标签选项

标签是名称/值值对，允许您对资源进行分类，并通过对多个资源和资源组应用相同的标签来查看合并的账单。

请注意，如果您在其他选项页上创建标签并更改资源设置，您的标签将自动更新。

![](img/ecf1b6d3def03c95166d6223c24cb862_135_0.png)

## 查看并创建

现在查看您的所有步骤并创建 Azure 应用。

## 创建 Web 应用

- 基础 部署 网络 监控 标签 | 查看 - 创建

摘要

- Web 应用

  由 Microsoft 提供

详情

| 字段 | 值 |
| :--- | :--- |
| 订阅 | 27d5f4a1-b6e4-4a12-b2d7-c1d2f1164ed8 |
| 资源组 | DOTNET-Test-Group |
| 名称 | DOTNET-Auth-api |
| 运行时堆栈 | .NET 8 LTS |
| 标签 | DOTNET-DEV-Auth |

App Service 计划（新建）

| 字段 | 值 |
| :--- | :--- |
| 名称 | DOTNET-Auth-api |
| 操作系统 | Windows |

下一步 > 下载自动化的模板。

点击创建按钮，然后 Azure 应用进程将开始。

## 创建 Web 应用

App Service 计划（新建）

| 字段 | 值 |
| :--- | :--- |
| 名称 | DOTNET-Auth-api |
| 操作系统 | Windows |
| 区域 | UAE North |
| SKU | Basic |
| 大小 | S11vU |
| 内存 | 1.75 GB 内存 |
| 标签 | DOTNET-DEV-Auth |

监控

| 特性 | 状态 |
| :--- | :--- |
| Application insights | 未启用 |

部署

| 特性 | 状态 |
| :--- | :--- |
| 持续部署 | 未启用 / 在应用应用后设置 |

下一步 > 下载自动化的模板。

您可以从下面的图中看到应用部署过程正在进行。

![](img/ecf1b6d3def03c95166d6223c24cb862_137_0.png)

现在您可以看到我们的部署过程已成功，我们可以进入已创建的资源。

![](img/ecf1b6d3def03c95166d6223c24cb862_137_1.png)

我们的 Azure 应用创建过程已完成。

## DOTNET-Auth-API

现在您需要点击 Azure URL。

## 应用程序状态

现在您可以看到我们的应用程序已经在 Azure 云上上线了。

## Microsoft Azure

## 您的应用正在运行并等待您的内容

您的应用已上线，但我们还没有您的内容。如果您已经部署了，您的内容可能需要 5 分钟才能显示。请稍后回来。

- 支持 Node.js、Java、.NET 等更多

尚未部署过？

使用部署中心发布您的代码或设置部署

正在启动新的 Web 应用？

遵循我们的快速入门指南，在几分钟内准备好 Web 应用

## 发布配置文件

现在您需要点击 Azure URL。

## 应用程序状态

DOTNET-Auth-API

- .NET 配置文件。

![](img/ecf1b6d3def03c95166d6223c24cb862_139_0.png)

# 部署

## 部署 概述

- 简介
- 部署过程
- 服务器配置
- 结论

## 简介

在本章中，我们将学习如何使用 Visual Studio 2019 部署 .net core 到服务器。

## 步骤 1 上的账户设置

部署 .net core 的第一步是在托管提供商处创建一个账户，并按照章节中的步骤操作。

- 在托管面板中创建一个网站。
- 然后使用托管面板创建网站

## 步骤 2 在 Visual Studio 中创建

使用 Visual Studio 创建 .net core 5 版本。

![](img/ecf1b6d3def03c95166d6223c24cb862_146_0.png)

## 步骤 3 在应用程序中设置服务器数据库连接字符串

在您的应用程序 `appsettings.json` 中设置 Live 连接字符串
