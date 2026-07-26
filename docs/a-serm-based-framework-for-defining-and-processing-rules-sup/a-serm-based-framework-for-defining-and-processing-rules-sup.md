# 一种用于数据一致性与完整性验证的规则定义与处理 SERM 框架








![](img/87125e6b6a6b0a342ed962217596f951_0_0.png)

![](img/87125e6b6a6b0a342ed962217596f951_0_1.png)





# 基于 SERM 的定义和处理支持数据一致性与完整性验证的规则框架

Magdalena Krakowiak a, Pawel Ziemba b,*

> *“a波兰 Paradis大学，Tratralna 23, 64-600 Gorzów Wielkopolski
ᵇ波兰 什切青大学管理学院，Aleja Papieza Jawa II 22, 70-453 Szczecin

# 摘要

SERM（结构化实体关系数据）模型是经典 ER（实体关系）模型的分层扩展。SERM 图的分层结构意味着任何闭环关系都可能导致不性和缺乏数据完整性。这些问题的发生是不确定的，应当进行系统的研究。迫切需要开发一种支持定义控制实体的规则的方法。本文旨在介绍一种支持关系型数据库智能设计的框架。其主要方面包括基于 SERM 模型的逻辑规则的识别和语义对齐。该方法的一个重要优势是它不仅局限于构建语义数据库，还利用它设计数据库编程对象（如存储过程、函数和触发器），以维护一致性。


关键词：SERM 语义数据模型；逻辑规则；数据库编程对象；规则函数

# 1. 引言

关系数据库随 20 世纪代关系模型的出现而诞生。随后的技术发展促进了新数据模型的引入 [2][4][6]，但与趋势对应的模型已成功应用于许多现代商业系统中。应用的高数量和多样性证实了关系数据库的实用性 [9]，领先的 IT 制造商以关系数据库管理系统的形式支持并开发其产品。首先应该提到 Oracle（Oracle 数据库的创建者）[12] 或 Microsoft（SQLServer 的创建者）[11][17]。

* 通讯作者。电话：+48-91-444-1942。
邮箱：pawel.ziemba@usz.edu.pl


关系模型的广泛使用导致特定的现实可以在实体以及它们之间的关系中非常自然地表示 [6]。语义数据模型以 ER（实体关系图）的形式呈现了建模的片段 [1][2][3]。自 1989 年以来，它是概念设计的唯一实现方式。然而，数据库完整性和复杂性的增加显示了其局限性，从而促成了 SERM（结构化实体）模型形式的 ER（实体关系）模型的开发 [14]。应特别关注其图的结构，该结构基于继承层次结构和确定关系复杂度的方法——记法 (min, max)。SERM 模型的上述属性使设计人员和数据库分析师能够执行语义验证和数据分析 [15][19]。关系数据库的最佳结构不能完全保护其不受数据不一致性的影响 [21]。对于数据之间存在强依赖关系的模型尤其如此。因此，识别所有对数据完整性的威胁并反它们非常重要。逻辑规则在这里起着重要作用，因为它们定义了数据输入并存储在数据库后的一致条件。处理这些规则对于实现完整性至关重要。这涉及数据库中映射关系数据的语义一致性方面。

本文介绍了一个支持逻辑规则识别并通过在 MS SQL Server 中创建对象模板对其进行半自动处理的框架 [11][17]。规则以逻辑 if-else 语句的形式编码。所提出的框架基于透明的分层 SERM 系统图，但并未将数据库设计局限于创建其关系结构。Transact-SQL 半自动函数和触发器的引入使得该解决方案变成了一种支持数据库数据一致性和完整性验证的某种智能系统。这很重要，因为数据一致性和完整性问题是不确定的——它们可能发生也可能不发生。所提的方法允许检测 SERM 模型中的潜在敏感数据和关系环。该框架通过识别不一致性支持与数据库相关的决策。本文分为五部分。第 2 部分介绍了背景以及 SERM 与 ER 模型之间的差异。第 3 部分介绍了框架。第 4 部分是其实用示例。文章以结论和后续工作结束。

# 2. SERM 与 ER 模型的比较

SERM 模型是 ER 模型的扩展 [8]。与经典 ER 模型不同，SERM 模型通过其层次性质允许更复杂的结构。SERM 图的分层结构意味着任何闭环关系都可能导致不性和缺乏数据完整性。这些问题的发生是不确定的，应当进行系统的研究。迫切需要开发一种支持定义控制实体的规则的方法。本文旨在介绍一种支持关系型数据库智能设计的框架。其主要方面包括基于 SERM 模型的逻辑规则的识别和语义对齐。该方法的一个重要优势是它不仅局限于构建语义数据库，还利用它设计数据库编程对象（如存储过程、函数和触发器），以维护一致性。

语义数据模型以 ER（实体关系图）的形式呈现了建模的片段 [1][2][3]。自 1989 年以来，它是概念设计的唯一实现方式。然而，数据库完整性和复杂性的增加显示了其局限性，从而促成了 SERM（结构化实体）模型形式的 ER（实体关系）模型的开发 [14]。应特别关注其图的结构，该结构基于继承层次结构和确定关系复杂度的方法——记法 (min, max)。SERM 模型的上述属性使设计人员和数据库分析师能够执行语义验证和数据分析 [15][19]。关系数据库的最佳结构不能完全保护其不受数据不一致性的影响 [21]。对于数据之间存在强依赖关系的模型尤其如此。因此，识别所有对数据完整性的威胁并反它们非常重要。逻辑规则在这里起着重要作用，因为它们定义了数据输入并存储在数据库后的一致条件。处理这些规则对于实现完整性至关重要。这涉及数据库中映射关系数据的语义一致性。

关系模型的广泛使用导致特定的现实可以在实体以及它们之间的关系中非常自然地表示 [6]。语义数据模型以 ER（实体关系图）的形式呈现了建模的片段 [1][2][3]。自 1989 年以来，它是概念设计的唯一实现方式。然而，数据库完整性和复杂性的增加显示了其局限性，从而促成了 SERM（结构化实体）模型形式的 ER（实体关系）模型的开发 [14]。应特别关注其图的结构，该结构基于继承层次结构和确定关系复杂度的方法——记法 (min, max)。SERM 模型的上述属性使设计人员和数据库分析师能够执行语义验证和数据分析 [15][19]。关系数据库的最佳结构不能完全保护其不受数据不一致性的影响 [21]。对于数据之间存在强依赖关系的模型尤其如此。因此，识别所有对数据完整性的威胁并反它们非常重要。逻辑规则在这里起着重要作用，因为它们定义了数据输入并存储在数据库后的一致条件。处理这些规则对于实现完整性至关重要。这涉及数据库中映射关系数据的语义一致性。

# 3. 规则识别与处理框架

本文介绍了一个支持逻辑规则识别并通过在 MS SQL Server 中创建对象模板对其进行半自动处理的框架 [11][17]。规则以逻辑 if-else 语句的形式编码。所提出的框架基于透明的分层 SERM 系统图，但并未将数据库设计局限于创建其关系结构。Transact-SQL 半自动函数和触发器的引入使得该解决方案变成了一种支持数据库数据一致性和完整性验证的某种智能系统。这很重要，因为数据一致性和完整性问题是不确定的——它们可能发生也可能不发生。所提的方法允许检测 SERM 模型中的潜在敏感数据和关系环。该框架通过识别不一致性支持与数据库相关的决策。

### 3.1 框架流程图

操作算法如图 1 所示（注：文本中未提供图片）。






Magdalena Krakowiak 等人. / Procedia Computer Science 207 (2022) 4227–4236

### 3.2 编程对象模板

对于每个定义的规则，二值函数应返回逻辑语句（规则的头部）的值，即确认满足或未满足条件。由于 Transact-SQL 中没有逻辑数据类型 [11][17]，该模板使用了位（bit）类型。以下是基于 SERM 图的关系系统所开发出的规则模式形式：

```sql
CREATE FUNCTION rule, rule_function(
  @sensitive_data_1 [data_type],
  @sensitive_data_2 [data_type]
)
RETURNS bit
AS
DECLARE @met bit
if (condition)
  SET @met=1
else
  SET @met=0
RETURN @met
```

图 1. 基于 SERM 模型的识别和处理逻辑规则的框架。

该函数用于在分析电路上选定的发布操作表中。对于敏感表，在检查是否满足规则之前，会阻止添加和修改敏感数据的指令。只有当相应的规则返回值 1（TRUE）时，才允许执行上述添加新记录和更改现有记录的操作。对于敏感数据，如果有任何操作，在执行给定条件的操作和修改后可以删除状态。请注意，这些表来自继承层次的第一步（图的左侧），当存在依赖对象时，会通过默认限制 [11][12][17] 清除。这种控制通过为敏感表定义函数值来实现。当函数返回值 0（FALSE）时，意味着之前输入的数据现在威胁到数据库一致性，因为它们不再符合规则条件。此时应该删除该记录，但由于其他条件关系这是不可行的。因此，可以选择性生成条件表的触发器，但在大多数情况下使用它们并没有根据。

与条件表触发器不同，敏感表触发器是强制性的编程对象。在该框架开发的这些过程模板使用 Transact-SQL 语言 [11][17] 编写，并包含规则函数。

下面展示了两种自动生成的触发器模式：

- 控制敏感数据的记录编辑

```sql
CREATE TRIGGER [db].[Blocking_addition_of_sensitive_data]
ON [db][sensitive table]
INSTEAD OF INSERT
AS
BEGIN
SET NOCOUNT ON;
DECLARE @sensitive_data_1 [data_type]
DECLARE @sensitive_data_2 [data_type]
SELECT @sensitive_data_1 = sensitive_data_1, @sensitive_data_2 = sensitive_data_2 FROM inserted
if dbo.rule_function(@sensitive_data_1 , @sensitive_data_2)=1
    INSERT INTO [sensitive table] SELECT * FROM inserted
else
    RAISERROR ('The data do not satisfy the conditions of the rule', 16,10)
END
```

- 控制敏感数据的编辑

```sql
CREATE TRIGGER [db][Blocking_edition_of_sensitive_data]
ON [db][sensitive table]
INSTEAD OF UPDATE
AS
BEGIN
SET NOCOUNT ON;
DECLARE @sensitive_data_1 [data_type]
DECLARE @sensitive_data_2 [data_type]
DECLARE @id_sensitive_table [data_type]
if update(@sensitive_data_1) OR update(@sensitive_data_2)
BEGIN
SELECT @sensitive_data_1 = sensitive_data_1, @sensitive_data_2 = sensitive_data_2 FROM inserted
SELECT @id_sensitive_table = id_sensitive_table FROM deleted
if dbo.rule_function(@sensitive_data_1 , @sensitive_data_2)=1
    UPDATE [sensitive table] SET sensitive_data_1=@sensitive_data_1, sensitive_data_2=@sensitive_data_2
    WHERE id_sensitive_table=@id_sensitive_table
else
    RAISERROR ('The data do not satisfy the conditions of the rule', 16,10)
END
```

# 案例研究 – 患者服务系统模型

患者服务系统 (PSS) 涵盖了一个专家中心网络，这些中心提供医疗咨询和简单治疗等医疗服务。患者是客户的员工，即签署了此类服务提供合同的公司。各种专业的医疗人员按照每周入院计划工作，计划上记录了患者的访问情况。在第一次就诊期间，会进行访谈，包括病史、用药和患者过敏史。每次就诊注册都会添加诊所网络提供的服务，其价值等于开具的发票金额，加上就诊期间额外执行的服务。除了访谈数据外，患者卡还载有就诊记录，包括检查结果、处方、转诊单、假条、医生建议以及诊断结果。上述系统的语义模型如图 SERM 图（图 2）所示，这将是所提框架实现的基础。

## 4.1 闭合关系电路的识别与分析

在图 2 所示图中，我们可以区分出七个闭合关系电路。表 1 展示了包含在电路对象的名称和继承层次结构。对于每个电路，潜在的条件表和敏感表用**粗体**标记。根据开发的方法，只有位于电路最右侧的表（即属于继承层次最高层级的表）可能是敏感的。潜在条件表的确定取决于电路的布局。在提取电路中最左侧的元素的情况下（在电路 3,4 和 5 的情况下），条件表可能完全独立依赖于该元素。在分析的图中，电路 3、4 和 5 是一个特殊情况，其中可以作为条件表的对象是一个潜在的敏感表，因为缺少其他电路元素（电路中仅包含三个表）。当闭合电路中左侧对象的连接清晰可见时，这种连接是敏感的。

在各个电路中选定的潜在条件表和敏感表是分析它们之间关系的基础，以便定义可能的逻辑规则。在给出的示例中，作为分析结果显示了两个依赖关系。第一个涉及电路 1，与控制医疗人员的权利有关。患者为他有权享受的特定服务向某员工预约。第二个依赖情况在电路 4 中检测到，确保了对额外服务的控制。提供的额外服务不能与已预约的就诊相同。

表 1. 患者服务系统 SERM 图中的闭合关系电路（自绘）。

| 电路编号 | I | II | III | IV | V | VII |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | service | medical worker | worker's service | appointment schedule | appointment | |
| 2 | | medication | patient | appointment | prescription | prescribed medication |
| 3 | city | customer | patient | | | |
| 4 | service | | | | service provided | |
| 5 | | | | patient | appointment | referral |
| 6 | illness | | | pass illness | appointment | diagnosis |
| 7 | | clinic | surgery patient | appointment schedule | appointment | |

## 4.2 分析得出的规则函数

基于所提框架（图 1），为了定义规则函数，必须确定某些条件和敏感数据。根据在电路 1 中检测到的依赖关系，条件数据必须是员工标识符 (`id_worker`) 以及来自员工服务表的其有权享受的服务标识符 (`id_service`)。这些数据构成了 if-else 规则体。另一方面，敏感数据是预约表中的员工计划标识符 (`id_schedule`) 和其有权享受的服务标识符 (`id_service`)。这些数据是支持防止未经授权访问规则函数的参数。在这种情况下，该函数旨在保护患者免受向未经授权的员工预约服务。




Mag Magdalena Krakowska et al. / Procedia Computer Science 207 (2022) 4227-4236

第二个独立依赖关系与额外服务的注册以及保护患者免受已注册服务的重复付费有关。条件是预约表中的服务标识符 (`id_service`)，敏感数据是访问标识符 (`id_appointment`) 和由服务表提供的额外服务标识符 (`id_service`)。控制额外服务的规则函数在 `id_service` 参数的值等于对应于 `id_appointment` 的给定条件（对应于 `id_appointment` 参数）时，返回 0。额外服务控制函数采用以下结构（对应一种模式）：

```
CREATE FUNCTION control_of_additional_services
@id_service smallint,
@id_appointment smallint
RETURNS bit
AS
BEGIN
DECLARE @met bit
if not exists (SELECT * FROM appointment WHERE id_appointment=@id_appointment AND id_service=@id_service)
    SET @met=1
else
    SET @met=0
RETURN @met
END
```

## 4.3 使用规则函数的触发器

规则函数主要定义用于确保输入数据一致性的触发器。因此，它们基于敏感表并控制 `Insert` 和 `Update` 语句。每个电路规则中包含的依赖由一个函数处理。对于每个函数，都根据 3.2 节中提出的开发的模板生成两个存储过程。下面的触发器仅在规则函数返回值 1 时允许添加新记录。

```
CREATE TRIGGER [dbo][Control_add_visit]
ON [dbm][appointment]
INSTEAD OF INSERT
AS
BEGIN
SET NOCOUNT ON;
DECLARE @id_service smallint
DECLARE @id_schedule smallint
SELECT @id_schedule=id_schedule,@id_service=id_service FROM inserted
if dbo.control_of_rights(@id_schedule,@id_service)
    INSERT INTO inserted Select * FROM inserted
else
    RAISERROR ('The worker has no right to perform this service!', 16,10)
END
```

```
CREATE TRIGGER [dbo][Control_add_service]
ON [dbm][service provided]
INSTEAD OF INSERT
AS
BEGIN
SET NOCOUNT ON;
DECLARE @id_appointment smallint
DECLARE @id_service smallint
SELECT @id_appointment=id_appointment,@id_service=id_service FROM inserted
if dbo.control_of_additional_services(@id_service,@id_appointment)=1
    INSERT INTO [service provided] Select * FROM inserted
else
    RAISERROR ('This is recorded service for this visit!', 16,10)
END
```

Magdal Krakowska et al. / Procedia Computer Science 207 (2022) 4227–4236

第二类触发器是那些仅在规则函数返回值时允许更改敏感数据的触发器。每个电路的两个存储过程使用 `[dbo]`：

```
CREATE TRIGGER [dbo][Control_edit_visit]
 [dbo][appointment]
INSTEAD OF UPDATE
AS
BEGIN
    SET NOCOUNT ON;
    DECLARE @id_service smallint
    DECLARE @id smallint
    IF update(appointment) OR update(service)
    BEGIN
        SELECT @id_schedule schedule, @id_service service FROM inserted
        SELECT @id_appointment appointment, @id service FROM deleted
        IF (dbo.check_of_right(@id_service, @id)=1)
            UPDATE schedule SET schedule=@id_schedule, service=@id_service
            WHERE @id_appointment = @id_appointment                ELSE
            RAISERROR ('The worker has no right to perform this service!', 16, 10)
    END
END
```

```
CREATE TRIGGER [dbo][Control_edit_service]
 [dbo][service]
INSTEAD OF UPDATE
AS
BEGIN
    SET NOCOUNT ON;
    DECLARE @id_service smallint
    DECLARE @id smallint
    DECLARE @id_service smallint
    DECLARE @id_old smallint
    IF update(appointment) OR update(service)
    BEGIN
        SELECT @id_appointment appointment, @id_service service FROM inserted
        SELECT @id_appointment appointment, @id_service service FROM deleted
        IF (dbo.check_of_additional(@id_service, @id)=1)
            UPDATE appointment SET appointment=@id_appointment, id=@id_id, service=@id_service
            WHERE @id_appointment=@id_appointment AND @id_old=@id_old
        ELSE
            RAISERROR ('This service is reserved for this service!', 16, 10)
    END
END
```

表触发器是一组生成的存储过程。这用于控制在删除记录或更改条件数据后的数据一致性。由于编辑（尤其是删除）数据，这是框架的一个可选阶段。这是为了分析用户需求并强制执行外键的值（NOT NULL）。在最左侧元素唯一的闭合电路的情况下，条件表充当特定角色，并且通常受到取消限制。在给出的示例中，分析的两个电路中有一个系统，其分析证实了这一点。在电路 4 中，条件表是预约表。一旦安排了预约并记录了额外服务，它就不能被删除，因此在更改后没有需要进行状态检查。在这种情况下，如果已注册服务的标识符发生变化，这在注册额外服务之前是可能的。因此，它是允许。

*(注：原文后续部分存在大量重复段落，已根据逻辑进行清理。)*
