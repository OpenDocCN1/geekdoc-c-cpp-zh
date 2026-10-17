
Team Foundation Server 管理员可能会说他们想从 Team Foundation Server 的旧版本迁移到 Team Foundation Server 2012。更有可能的是，他们的意思是想要升级到新版本。如果 Team Foundation Server 管理员选择了错误的方法，团队在过渡到 Team Foundation Server 2012 的过程中将面临数据丢失和更多工作量。

## 升级 (Upgrade)

“升级”一词是指使用 Team Foundation Server 配置向导，将数据从 Team Foundation Server 的旧版本移动到最新版本的过程。这种场景与设置一个新的 Team Foundation Server 2012 服务器并尝试将源代码和项目“移动”到新服务器中是不同的。升级是完全支持的，并在发布前已在许多配置中经过了测试。在升级过程中，服务器在数据库级别进行转换，并且所有数据和元数据都会被保留。

通过使用适当配置向导，该过程能够通过全保真升级（full-fidelity upgrade），以管理员和使用服务器的团队成员最少的精力保留所有的数据和历史。

还有不同类型的升级，例如：

- **原地升级（In-place upgrade）**——原地升级定义为完成后完成后继续使用运行当前 Team Foundation Server 的相同硬件set的升级。
- **基于迁移的升级（Migration-based upgrade）**——基于迁移的升级定义为涉及第二组重复硬件的升级，在过程完成后，该硬件将托管 Team Foundation Server 的新版本。注意，尽管名称相似，但基于迁移的升级并不是迁移。

> 注意：第 25 章探讨了与从旧版本升级 Team Foundation Server 过程相关的主题。

## 迁移 (Migration)

迁移是指将操作从一个系统重放到另一个系统的过程。其关键区别之一是，迁移是一种低保真度的数据传输。在 Team Foundation Server 中，只有版本控制和工作项跟踪数据可以迁移——构建数据、报告和其他元数据无法迁移。通常，可用的迁移工具所经过的测试远少于升级过程，且可用工具的支持有限（这些工具通常在正常发布周期之外单独发布）。

在迁移的情况下，数据转换仅使用公共 API 完成，而这些 API 限于在移动数据时提供某些信息。这种局限性导致的结果是某些数据在迁移过程中丢失或失真。示例包括构制品 ID（更改集编号、工作项 ID）、时间戳、区域路径（area paths）和迭代路径（iteration paths）。

> 注意：Team Foundation 版本控制团队的计划经理 Matthew Metrik 就这一特定概念写了多篇博客文章，并讨论了每种不同的场景。更多信息请访问 `http://aka.ms/TfsUpgradeOrMigration`。

## 迁移历史还是最新版本

团队必须做出的要决定之一是，你们是想从旧版版本控制系统迁移所有的源代码历史，还是只获取特定里程碑的最新版本（有时被称为 tip 版本）。大多数团队会立即回答：“我们需要历史。没有历史我们没法迁移。”

迁移历史的明显优势是能够立即看到随着时间推移而引入的历史。迁移到 Team Foundation Server 的另一个优势是可以停用旧服务器。

然而，将历史迁移到新系统也有潜在的劣势。以下是其中一些：

- **测试**——迁移应该像任何软件开发项目一样被对待。应该投入时间和精力在测试环境中多次测试迁移，以确保最终结果符合你的预期。
- **第三方购买**——你的团队可能想要使用市售的第三方工具。这涉及购买许可证以及可能与供应商签订的支持合同。
- **自定义开发**——可能还需要开发并测试自定义工具或 Team Foundation Server 适配器。
- **回放执行时间**——除了计划、开发和测试时间外，你必须考虑实际回放所有历史所需的时间。

最终，迁移源代码历史的投资回报应该被确定并与劣势进行权衡。如果团队最终只迁移了最新版本，始终可以让旧版版本控制系统处于只读状态，以便团队在需要时研究存档中的历史。

> 注意：关于此特定主题的更多信息，Developer Smackdown 播客的主及其嘉宾 Ed Blankenship 在一集中讨论了基础迁移，地址为 `http://aka.ms/EdPodcastMigration`。

## 从 VISUAL SOURCESAFE 迁移

如果团队目前在使用 Visual SourceSafe (VSS)，那么他们就幸运了。Team Foundation Server 2012 包含了一个简化的 VSS 源码升级工具，它可以将 VSS 存储库迁移到 Team Foundation 的项目中。

## VSSCONVERTER.EXE 去去哪里了？

在 Team Foundation 2012 中，`VSSConverter.exe` 工具已更新并重命名为 `VssUpgrade.exe`。与旨在简化常见升级场景的 VSS 升级向导不同，此工具允许更精细的控制。

该工具包含了向导目前不支持的若干功能，包括：

- 移动条目或指定的文件夹。
- 将旧存储库的位置映射到 Team Foundation Server 版本控制库的新位置。
- 在迁移开始前分析 VSS 存储库的损坏和其他迁移问题。
- 将 VSS 用户映射到活动目录 (AD) 域用户帐户。
- 在从 VSS 绑定迁移到相应的 Team Foundation Server 绑定期间更新 Visual Studio 解决方案和项目的绑定。

关于 `VssUpgrade.exe` 工具的更多信息，请参阅 `http://aka.ms/Tfs2012VssUpgrade`。

> 注意：Microsoft Visual SourceSafe 2005 标准版的主流支持已于2012 年 7 月 10 日结束。当微软结束对某个产品的主流支持时，它将停止发布非安全热补丁、提供电话支持并提供其他主流支持选项。某些公司可能可以通过某些扩展支持选项获得某些福利，但此类公司可能必须在主流支持结束后 90 天内采取行动以利用这些支持。关于 VisualSourceSafe2005 支持生命期的最新信息，请参阅 `http://aka.ms/SupportVSS`。公司也可以联系其微软代表，进一步询问主流支持后的支持选项。

VSS 升级向导在迁移过程中会将所有的签入（check-ins）回放到 Team Foundation 中。它通过为同一用户在同一时间提交且具有相同内容的文件创建更改集（changesets）来实现。此外，这些更改之间不能冲突，才能包含在同一个更改集中。例如，如果用户在相对相同的时间段内添加了一个特定文件又删除了它，那么这些操作将不会在同一个更改集迁移中提交。

你会注意到结果之一是新更改集的日期和时间戳将被设置为迁移实际发生的时间，而不是原始时间。原始签入日期和时间戳将存储在更改集中以供参考。此外，如果用户没有经过适当映射（如本节后半部分所述），原始用户将不在注释中。如果用户映射恰当，则用户名将是更改集的用户名字段。

本节将检查团队在他们想要将完整历史记录从 VSS 迁移到 Team Foundation Server 版本控制存储库时可以拥有的不同选项。

## 准备使用 VSS 升级向导

在尝试进行迁移工作之前，首要步骤是确保 VSS 仓库已完全备份。这使得在迁移过程中发生任何错误时能够将其恢复到原始状态。务必对数据库的副本运行迁移实用程序，而不是实际数据库。

关键之一是确保，如果 VSS 数据库旧于最新版本（Visual SourceSafe 2005），则应在迁移之前升级数据库。在安装 Visual SourceSafe 2005 后，可以使用 `DDUPUPD` 工具升级到最新版本。

在启动向导之前，一个重要的步骤是在您的 VSS 仓库上运行 VisualSource ANALYZE 工具。这将检查完整性并修复任何结构性错误。

> 注意：有关 VSS ANALYZE 工具的更多信息，请参阅 `http://aka.ms/VssAnalyze`。

您的开发团队可能选择不迁移 VSS 仓库中存储的所有历史记录，而是选择仅迁移历史记录的子集。您的团队可能决定只需要最近几年的历史，以减少迁移执行时间。如果是这样，管理员应该使用 VSS 中提供的归档功能对选择日期之前的所有内容进行存档。

> 警告：使用 VSS 中的归档功能将永久删除指定的源代码和历史。如果您需要保留这些数据，请确保在执行此步骤之前备份 VSS 数据库。

对于那些需要尽可能减少迁移执行时间的实例，请确保迁移中的所有服务器和计算机位于同一个局域网或同一个网络交换机上。迁移工作中将使用的服务器和计算机包括：执行 VSS 升级的迁移计算机、托管包含 VSS 数据库的文件共享服务器以及 Team Foundation。

最后，通过告知迁移发生的时间来为迁移做准备。例如，某些团队会在周五下班时开始迁移，以便迁移可以在周末期间执行，并在周一上班时可以使用新位置。理想情况下，团队将在迁移发生期间已签入所有文件、移除任何签出（check-outs），并且没有使用 VSS 数据库。为了确保只有升级向导可以访问存储库，可以从执行迁移的账户之外的所有用户移除文件共享权限。

## 使用 Visual SourceSafe 升级

一旦您准备好迁移，第一步就是下载并安装向导的最新副本。要执行此操作，打开 Foundation Server 管理控制台，导航到“其他工具和组件”，然后转到“Visual SourceSafe 升级”。在右侧，您将看到一个下载并安装最新版本的链接，如图 8-1 所示。

一旦下载了向导，运行 `tfs_VssUpgrade.exe` 启动安装程序。将出现安装向导屏幕，要求您输入安装路径并接受许可条款和条件，如图 8-2 所示。点击“安装”继续。

> 注意：为了进一步简化流程，安装程序包含了 Visual SourceSafe 对象模型。这意味着无需在执行迁移的机器上预安装 Visual SourceSafe 或其他先决条件。

## 从 VisualSourceSafe 迁移 | 183

![](img/aaf6096fc6b4485534c737801bdbc4fd_220_0.png) 图 8-1：管理控制台中的 VisualSourceSafe

![](img/aaf6096fc6b4485534c737801bdbc4fd_220_1.png) 图 8-2：VSS 安装程序

www.itooks.info

## 第8章 迁移遗留系统

一旦安装了向导，可以通过开始菜单下的 Studio 2012 Team Foundation 启动，或者通过运行安装路径下的 `Vss.exe` 启动。

在向导中，您需要提供以下内容：

- VisualSourceRepository——包含 `srcsafe.ini` 的文件夹。
- VisualSourceAdmin password（可选）——管理员账户的密码。

VSS 升级还需要一个 Server 实例。一旦您指定了有效的存储，就可以点击“列出”项目，如图 8-3 所示。当您准备好后，点击“下一步”。

![](img/aaf6096fc6b4485534c737801bdbc4fd_221_0.png) 图 8-3：VSS 升级选项

后续屏幕（图 8-4）要求您指定目标团队项目。要求此项目不包含任何源代码。点击“浏览”按钮选择适当的目标。点击“下一步”进入升级选项。

升级选项屏幕（图 8-5）允许您选择升级的完整度。有两个选项：

- 1. 完整历史（Full history）——迁移所有提交。
- 2. 提示（Tip）——仅迁移每个文件的最新版本。

## 从 VisualSourceSafe 迁移 | 185

![](img/aaf6096fc6b4485534c737801bdbc4fd_222_0.png) 图 8-4：目标团队项目屏幕

![](img/aaf6096fc6b4485534c737801bdbc4fd_222_1.png) 图 8-5：升级选项屏幕

www.itooks.info

VSS 升级向导在迁移过程中还需要一个 Server 实例进行临时存储。如果此 SQL 实例位于本地或靠近迁移机器则最好。这将减少延迟并确保迁移尽可能快地进行。

一旦您选择了升级选项和有效的 SQL 实例，点击“下一步”。在执行一系列检查后，点击“下一步”开始迁移过程。运行所需取决于取决于选择的选项以及更改的数量。向导会显示进度和正在执行的操作，如图 8-6 所示。

![](img/aaf6096fc6b4485534c737801bdbc4fd_223_0.png) 图 8-6：升级进度屏幕

一旦迁移过程完成，您将能够查看“升级报告”。此报告详细说明了迁移设置、合并的更改、文件和文件夹数量。报告还将显示任何遇到的警告或问题。您可以在图 8-7 中看到报告示例。

向导的局限性之一是 Team Foundation 中更改集的日期时间戳将是迁移发生的时间，而不是原始签入时间。然而，如图 8-8 所示，原始的 VSS 提交时间保留在更改集的注释中。

## 从 VisualSource 迁移 | 187

![](img/aaf6096fc6b4485534c737801bdbc4fd_224_0.png)

图 7：更新报告

![](img/aaf6096fc6b4485534c737801bdbc4fd_224_1.png)

图 8：显示原始 V 时间戳的视图

www.it-ebooks.com

## Team Foundation Server 集成平台

微软的 Team Foundation Server 产品拥有专门的资源，用于创建一个名为 Team Foundation Server 集成平台（TFS Integration Platform）的平台，该平台允许客户构建和同步工具。它本质上是一个完整的框架，提供了一个用于配置迁移/同步运行的用户界面 (UI)、用于执行操作的服务，以及当团队使用该工具处理迁移/同步操作时为团队提供的冲突解决体验。

微软在专门的 CodePlex 项目站点 `http://fsintegration.codeplex.com/` 上提供了免费实用程序和源代码。CodePlex 项目站点经常上传更新，Visual Studio ALM Rangers 还提供了一份可以快速上手的快速文档。图 8-9 是 Team Foundation Server 集成平台配置工具的截图。

![](img/aaf6096fc6b4485534c737801bdbc4fd_225_0.png)

图 8-9：Team Foundation Server 集成平台配置工具

Team Foundation Server 集成平台可以通过适配器系统协助将版本控制产物和工作项从旧系统迁移到 Team Foundation Server。Team Foundation Server 适配器已经创建，你只需要做的就是为旧系统创建一个版本控制或工作项跟踪适配器。

开箱提供了创建自定义适配器以及其他适配器的示例。以下是编写本文时可用的某些适配器：

- Team Foundation Server 2008、2010 和 2012 版本控制
- Team Foundation Server 2008、2010 和 2012 工作项跟踪
- RationalClearCase
- Rational ClearQuest
- SharePoint 列表
- SharePoint 文档库
- 文件系统

该框架的引入是为了用于为旧系统创建自定义适配器。CodePlex 站点列了该团队为流行的版本控制和项目跟踪产品创建适配器的待办事项。欢迎建议新系统，或者在 Issue Tracking 系统中对你认为团队应该创建适配器的系统进行投票（这些系统在 CodePlex 条目中已创建）。

如果你想从自定义的内部系统迁移，可以使用 Team Foundation Server 集成平台中提供的 API 创建自定义适配器。Team Foundation Server 集成平台的源代码中提供了两种类型适配器的示例，以帮助你开始。

> 注意：如本章前面提到的，某些项不使用该工具进行迁移，在决定工具是否满足你的需求时，应该考虑到这一点。内置适配器不会迁移以下产物：
>
> - 权限
> - 标签 (Labels)
> - 签存集 (Shelvesets)
> - 工作项查询
> - 文件编码
> - 待处理更改
> - 提交备注
> - 工作空间
> - 团队
> - 测试用例
> - 提交策略
> - 报告
> - 团队门户
> - 过程模板
> - 生成 (Builds)
> - 仓库项

## 流行的第三方迁移工具

市面上有几种商用的第三方工具，可以供那些没有可用工具，或者不想为 Team Foundation Server 平台构建自定义适配器的团队使用。让我们来看看其中几个。

## Subversion、CVS 和 StarTeam

Timely Migration 团队构建的一项工具非常成功地将源代码历史从 Subversion (SVN) 仓库迁移到 Team Foundation Server。它处理了许多常见情况，例如迁移完整历史或选定的历史、发现分支并在 Team Foundation Server 中创建分支，以及将标签转换为 Team Foundation 版本控制标签。

除了 SVN 之外，Timely Migration 工具还支持从 CVS 或 StarTeam 仓库迁移，并具有与 SVN 迁移工具类似的功能。

> **注意**：有关关于 Timely Migration 工具的更多信息，请访问网站 `http://aka.ms/Timelymigration`。该工具需要付费，此外测试和实际运行所需的任何支持小时也是收费。你可以下载该工具的试用版，这是一个功能完整的评估版本，允许你在购买产品之前测试迁移。然而，当它提交到 Team Foundation Server 时，它会混淆每个文件的内容。

## ClearCase

幸运的是，Team Foundation Server 集成平台包含一个适配器，允许团队从 IBM Rational ClearCase 源代码控制仓库迁移到 Team Foundation Server。你可以使用现有的适配器选择迁移完整历史或选定的历史。

本章前面介绍了关于 Team Foundation Server 集成平台的更多信息。
