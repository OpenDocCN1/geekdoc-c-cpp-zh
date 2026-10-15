

或行业标准应用程序，但对传统图书馆应用程序构成挑战。基于服务器的 PaaS 平台在很大程度上旨在满足中小型用户的需求，而基于应用程序的平台则旨在实现透明且高度可用。

## 参考文献

Bryant, Sally, and Grace Ye. 2012. "Implementing OCLC's WMS (Web-Scale Management Services) Circulation at Pepperdine University." Journal of Access Services 9 (no. 1): 1–17. doi:10.1080/15367967.2011.629921.

Code4Lib. 2012. "Anyone Implementing Common LIS Applications on PaaS Providers?" Code4Lib Listserv archive, March 29, 2012. http://serials.infomotions.com/code4lib/archive/2012/201203/0983.html.

De Wilde, Max. 2012. "Collective Access on Red Hat OpenShift." http://homepages.ulb.ac.be/~svhoolan/redhat_ca_install.pdf.

Hoofman, Matt. 2012. "Wordpress-Heroku." https://github.com/mhoofman/wordpress-heroku.

Liu, Cricket, and Paul Albitz. 2006. DNS and Bind. Sebastopol, CA: O'Reilly.

Loo, Jeffery. 2010. "Library Instruction through Online Video and Social Media." Chemistry and Chemical Engineering Library, University of California, Berkeley, last modified July 16, 2010. www.lib.berkeley.edu/CHEM/instruction/video/index.htm.

Matienzo, Mark A. 2012. "Blacklight on Heroku." https://github.com/projectblacklight/blacklight/wiki/Blacklight-on-Heroku.

OCLC. 2012. "University of Delaware Chooses OCLC Worldshare." OCLC press release, January 18. www.oclc.org/news/releases/2012/20125.htm.

Stein, T. J. 2011. "Running WordPress on Heroku + Amazon RDS." http://tjstein.com/2011/09/running-wordpress-on-heroku-and-amazon-rds/.

Van Hooland, Seth, and Bram Wierckx. 2011. Open Source Software Platform Collective Access as a Service Solution." DISH (Digital Strategies for Heritage) 2011 conference, December 7, Rotterdam, Netherlands.

## 基础设施即服务

对于有传统 IT 资源管理背景的图书馆来说，采用 IaaS 方法进行云计算很可能是不错的选择。IaaS 提供商简化了预订、启动和管理 IT 资源的过程，包括服务器、存储空间、网络工具和监控工具。这使得图书馆能够创建针对特定需求和应用程序量身定制的 IT 基础设施。此外，这些系统通常支持对特定资源进行定制，例如操作系统、应用程序平台、磁盘空间和内存。

与专用的 PaaS 系统一样，IaaS 系统需要在计算环境中投入一定程度的资源，并且有一些复杂元素，需要熟悉 IT 系统和开发平台，而这些并不是图书馆常见的技能组合。有了这种专业知识，利用 IaaS 资源创建和管理灵活且强大的计算环境的能力，可以从根本上改变图书馆寻求满足其 IT 需求的新方式。这也意味着 IaaS 解决方案需要比 PaaS 或 SaaS 解决方案更关注安全、备份和服务恢复程序，并且将确保可扩展性和可持续性的负担放在图书馆而不是云服务提供商身上。

在本章中，我们从两个角度回顾 IaaS 解决方案：使用 IaaS 资源复制传统服务架构，以及使用它们创建云感知服务架构。在深入探讨这些解决方案之前，值得先定义一些通用的资源类型，这些资源类型是每个 IaaS 解决方案共有的。以下列表可能很熟悉，但在整个章节中，它们为 IaaS 示例的讨论提供了背景。

### 32 位与 64 位操作系统
这些数字指的是操作系统运行的底层架构。这些不同的硬件架构需要不同的操作系统版本，能够进行不同程度的 CPU 和内存管理。许多 IaaS 提供商根据所选的服务器大小确定操作系统的类型，并使用某种方法自动将 32 位系统扩展到 64 位系统。然而，Amazon 确实支持在 32 位平台上运行 64 位计算映像，因此如果需要扩展到更大服务器，最好选择 64 位操作系统发行版。

### 应用程序编程接口 (API)
在云环境中，API 是一种用于与 Web 服务交互的标准化的程序化机制。所有 IaaS 提供商都提供某种形式的 API，并且通常通过实现 API 功能的程序化工具提供增强的服务和功能。人们正在努力开始使用开源方法标准化云 API。

### 备份/恢复
IaaS 提供商通常具有某种系统范围的方法来处理服务器和存储空间备份。一些供应商提供托管备份解决方案（例如，Linode）；其他供应商仅提供云基础设施备份工具（例如，Amazon）。

### 带宽/进出传输
IaaS 供应商监控并对服务器实例的进出流量收费。向入站流量收费的情况变得越来越少，但本章讨论的所有供应商都对出站流量收费。一些供应商（例如，Linode）会在服务器实例中包含基础数据传输量。

### 云文件系统
云文件系统与传统文件系统不同之处在于，它们可通过 API 访问，而不是通过传统的磁盘或挂载机制。云文件系统可能具有自动复制、版本控制和其他增值服务，使其比传统存储更可靠。

### 配置配置文件
配置配置文件是一组促进云资源配置和部署的指令。这是 IaaS 提供商的新兴功能，并且在每个 IaaS 解决方案中实现方式不同。其基本概念与 Puppet 和 Chef 等自动配置平台类似，只是

它们往往仅在系统启动期间使用，而不是持续使用。

### 域名服务 (DNS)
DNS 是一种全球互联网应用程序，可将域名（mycompany.com）解析为 IP 地址（10.10.10.10）。云提供商提供针对云用户特定需求的 DNS 解决方案，例如多区域路由。

### 端点
在云计算中，端点是私有云与互联网相遇的点。Amazon 提供多个云区域，每个区域都充当其内部云流量的端点。

### 文件存储桶/容器
存储桶或容器是与基于云的文件系统相关的存储单元。文件只能在与特定存储桶或容器关联后上传。云提供商还可能将访问控制与存储桶或容器关联。

### 负载均衡器
云提供商通常支持某种自动方法来实现负载均衡应用程序。负载均衡器监控给定服务的流量，并在需要时重新路由流量或扩展服务器资源。

### 机器映像
机器映像是 IaaS 环境中启动服务器的根源。一些提供商（例如，Amazon）允许用户在社区门户中上传、发布和下载映像；其他提供商（例如，Rackspace、Linode）提供较小的经过审核的机器映像套件。所有服务都提供某种机制，可将自定义机器映像保存到客户的云服务中以供重复使用或重新利用。

### 消息或队列服务
这些服务为向用户或应用程序发送消息提供独立的手段。Amazon 提供多种形式，包括简单电子邮件服务（SES）和简单通知服务（SNS）。消息服务可以取代在机器映像上运行传统电子邮件和其他消息服务的需要。

### 可挂载卷
一些 IaaS 提供商提供更传统的存储形式，可作为服务器资源的磁盘或卷挂载。Amazon 的这种存储形式（弹性块存储，EBS）具有用户控制的大小、格式、附加/分离服务和长期存储功能。

### 公钥/私钥
除了基于密码的安全性外，云提供商还可能支持生成或使用公钥/私钥进行资源

