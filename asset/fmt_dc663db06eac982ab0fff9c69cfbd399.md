
## 图和递归查询

本章涵盖了 Microsoft SQL Server 中对名为“图”（graphs）的特殊数据结构的处理。人们在讨论图时会使用不同的术语，如层级结构（hierarchy）和树（tree），但这些术语经常被误用。因此，本章从描述图及其属性的术语开始，以消除困惑。

在关系型数据库管理系统 (RDBMS) 中对图的处理远非易事。我将讨论两种主要方法。一种是基于迭代或递归逻辑——例如使用递归查询。另一种是基于在数据库中物化描述数据结构的额外信息——例如使用 `HIERARCHYID` 数据类型。

## 术语

本章使用了许多术语来讨论图以及如何在 SQL Server 中操纵它们。本节提供了重要术语的定义，以确保你理解它们。

> 注意：本节的解释基于美国标准与技术研究院 (NIST) 的定义。我对原始定义进行了一些修订，并添加了一些叙述，使其显得不那么正式，并保持与主题领域（T-SQL）相关。有关图及相关术语更完整、更正式的定义，请参考 http://www.nist.gov/dods/

## 图

图是一个由边（edges）连接的项集。每个项被称为顶点（vertex）或节点（node）。边是图中两个节点之间的连接。

“图”是数据结构的一种统称，许多场景都可以表示为图——例如，员工组织架构、物料清单 (BOMs)、道路系统等。为了将图的类型缩小到更具体的案例，你需要识别它的属性：

- **有向/无向**：在有向图（也称为 digraph）中，边的两个节点具有方向或顺序——其中一个是主节点，另一个是次要节点。

例如，对于咖啡店产品的 BOM 图，你可能拥有名为“Latte（拿铁）”和“Milk（牛奶）”的节点。但你不能反转这种关系。对于节点对 (Latte, Milk)，图有一条边（包含关系），但对于节点对 (Milk, Latte) 则没有边。

在无向图中，每条边都简单地连接两个节点，没有特定的顺序。例如，道路系统图可以有一条连接洛杉矶和旧金山的道路。节点（城市）洛杉矶和旧金山（或旧金山、洛杉矶）之间的边（道路）。

- **无环/有环**：无环图是没有循环的图——即没有起点和终点同一个节点的路径。示例包括员工组织架构和 BOM。有向无环图被称为 DAG。

如果图中具有起点和终点同一个节点的路径——道路系统中通常是这样——那么该图就是有环的。

## 树

树是从根节点开始访问的数据结构。每个节点要么是叶节点要么是内部节点。内部节点具有一个或多个子节点，并被称为子节点的父节点。同一节点的所有子节点都是兄弟。树是无环图。与物理树的外相反，根通常显示在结构的顶部，而叶节点显示在底部，如图 11-1 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_732_0.png)

**图 11-1** 树中节点的作用。

森林是一个多个树集合——例如，论坛讨论可以表示为森林，其中每个线程都是一棵树。

## 层级结构

某些场景可以被描述为层级结构，并建模为有向无环图（DAG）——例如面向对象编程中类型和类之间的继承关系，以及员工组织架构图中的汇报关系。在第一种场景中，图的边确定了继承关系。类可以从其他类继承方法和属性（并可能从多个类继承）。在后一种场景中，边表示员工之间的汇报关系。请注意这些场景具有有向且无环的特性。例如，公司的管理责任链是不可能形成循环的。

## 场景

在整个章节中，我将使用三个场景：员工组织架构图（树、层级结构）；物料清单，简称 BOM（有向无环图 DAG）；以及道路系统（无向环图）。请注意（有向）根树与有向无环图（DAG）的区别。所有的树都是 DAG，但并不是所有的 DAG 都是树。在树中，一个项目最多有一个父节点。

# 员工组织架构图

我将使用的员工组织架构图如图 11-2 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_733_0.png)

图 11-2 员工组织架构图。

要创建 Employees 表并填充示例数据，请运行列表 11-1 中的代码。Employees 表的内容如表 11-1 所示。

## 列表 11-1 Employees 表的定义语言和示例数据

```sql
SET NOCOUNT ON;
USE tempdb;
IF OBJECT_ID(N'dbo.Employees', 'U') IS NOT NULL DROP TABLE dbo.Employees;
GO
CREATE TABLE dbo.Employees (
  empid INT NOT NULL CONSTRAINT PK_Employees PRIMARY KEY,
  mgrid INT NOT NULL CONSTRAINT FK_Employees_Employees REFERENCES dbo.Employees,
  epname VARCHAR(25) NOT NULL,
  salary MONEY NOT NULL,
  CHECK (empid > mgrid)
);

INSERT INTO dbo.Employees(empid, mgrid, epname, salary) VALUES
(1, NULL, 'David', 10000.00),
(2, 1, 'Eitan', 7000.00),
(3, 1, 'Ina', 7500.00),
(4, 2, 'Seraph', 5000.00),
(5, 2, 'Jiru', 5500.00),
(6, 2, 'Steve', 4500.00),
(7, 3, 'Aaron', 5000.00),
(8, 5, 'Lilach', 3500.00),
(9, 7, 'Rita', 3000.00),
(10, 5, 'Sean', 3000.00),
(11, 7, 'Gabriel', 3000.00),
(12, 9, 'Emilia', 2000.00),
(13, 9, 'Michael', 2000.00),
(14, 9, 'Didi', 1500.00);

CREATE UNIQUE INDEX idx_un_mgrid_empid ON dbo.Employees(mgrid, empid);
```

## 表 11-1 Employees 表的内容

| empid | mgrid | epname | salary |
|---|---|---|---|
| 1 | NULL | David | 10000.000 |
| 2 | 1 | Eitan | 7000.000 |
| 3 | 1 | Ina | 7500.000 |
| 4 | 2 | Seraph | 5000.000 |
| 5 | 2 | Jiru | 5500.000 |
| 6 | 2 | Steve | 4500.000 |
| 7 | 3 | Aaron | 5000.000 |
| 8 | 5 | Lilach | 3500.000 |
| 9 | 7 | Rita | 3000.000 |
| 10 | 5 | Sean | 3000.000 |
| 11 | 7 | Gabriel | 3000.0000 |
| 12 | 9 | Emilia | 2000.0000 |
| 13 | 9 | Michael | 2000.0000 |
| 14 | 9 | Didi | 1500.0000 |

Employees 表以邻接列表的形式表示管理层级，其中经理和员工分别代表父节点和子节点。

## 物料清单 (BOM)

我将使用一个咖啡馆产品的物料清单，如图 11-3 所示。

![](img/bdc38aa36f6e2987d913ee5381474711_735_0.png)

图 11-3 咖啡馆产品的物料清单 (BOM)。

要创建 Parts 和 BOM 表并填充示例数据，请运行列表 11-2 中的代码。Parts 和 BOM 表的内容如表 11-2 和 11-3 所示。注意，第一个场景（员工组织图）只需要一张表，因为它被建模为树；边（经理，员工）由同一行表示。而 BOM 场景需要两张表，因为它被建模为 DAG，多个路径可以指向同一个节点。边（组装，零件）由 BOM 表中的行表示，节点由 Parts 表中的行表示。

## 列表 11-2 Parts 和 BOM 表的定义语言和示例数据

```sql
IF OBJECT_ID(N'dbo.BOM', 'U') IS NOT NULL DROP TABLE dbo.BOM;
IF OBJECT_ID(N'dbo.Parts', 'U') IS NOT NULL DROP TABLE dbo.Parts;
GO
CREATE TABLE dbo.Parts
(
  partid INT NOT NULL CONSTRAINT PK_Parts PRIMARY KEY,
  pathname VARCHAR(25) NOT NULL
);

INSERT INTO dbo.Parts(partid, pathname) VALUES
(1, 'Black Tea'),
(2, 'White Tea'),
(3, 'Latte'),
(4, 'Espresso'),
(5, 'Double Espresso'),
(6, 'Cup Cover'),
(7, 'Regular Cup'),
(8, 'Stirrer'),
(9, 'Espresso Cup'),
(10, 'Tea Shot'),
(11, 'Milk'),
(12, 'Coffee Shot'),
(13, 'Tea Leaves'),
(14, 'Water'),
(15, 'Sugar Bag'),
(16, 'Ground Coffee'),
(17, 'Coffee Beans');

CREATE TABLE dbo.BOM
(
  partid INT NOT NULL CONSTRAINT FK_BOM_Parts REFERENCES dbo.Parts,
  assemblyID INT NOT NULL CONSTRAINT FK_BOM_Parts REFERENCES dbo.Parts,
  unit VARCHAR(5),
  qty DECIMAL(8, 2) NOT NULL,
  CONSTRAINT UK_BOM (partid, assemblyID),
  CONSTRAINT CHK_BOM (partid <> assemblyID)
);

INSERT INTO dbo.BOM(partid, assemblyID, unit, qty) VALUES
(1, NULL, 'EA', 1.00),
(2, NULL, 'EA', 1.00),
(3, NULL, 'EA', 1.00),
(4, NULL, 'EA', 1.00),
(5, NULL, 'EA', 1.00),
(6, 1, 'EA', 1.00),
(7, 1, 'EA', 1.00),
(10, 1, 'EA', 1.00),
(14, 1, 'ml', 230.00),
(6, 2, 'EA', 1.00),
(7, 2, 'EA', 1.00),
(10, 2, 'EA', 1.00),
(14, 2, 'ml', 205.00),
(11, 2, 'ml', 25.00),
(6, 3, 'EA', 1.00),
(7, 3, 'EA', 1.00),
(11, 3, 'ml', 225.00),
(12, 3, 'EA', 1.00),
(9, 4, 'EA', 1.00),
(12, 4, 'EA', 1.00),
(12, 5, 'EA', 2.00),
(13, 10, 'g', 5.00),
(14, 10, 'ml', 20.00),
(14, 12, 'ml', 20.00),
(16, 12, 'g', 15.00),
(17, 16, 'g', 15.00);
```

## 表 11-2 Parts 表的内容

| partid | partname |
|---|---|
| 1 | Black Tea |
| 2 | White Tea |
| 3 | Latte |
| 4 | Espresso |
| 5 | Double Espresso |
| 6 | Cup Cover |
| 7 | Regular Cup |
| 8 | Stirrer |
| 9 | Espresso Cup |
| 10 | Tea Shot |
| 11 | Milk |
| 12 | Coffee Shot |
| 13 | Tea Leaves |
| 14 | Water |
| 15 | Sugar Bag |
| 16 | Ground Coffee |
| 17 | Coffee Beans |

## 表 11-3 BOM 表的内容

| partid | assemblyid | unit | qty |
|---|---|---|---|
| 1 | NULL | EA | 1.00 |
| 2 | NULL | EA | 1.00 |
| 3 | NULL | EA | 1.00 |
| 4 | NULL | EA | 1.00 |
| 5 | NULL | EA | 1.00 |
| 6 | 1 | EA | 1.00 |
| 7 | 1 | EA | 1.00 |
| 10 | 1 | EA | 1.00 |
| 14 | 1 | ml | 230.00 |
| 6 | 2 | EA | 1.00 |
| 7 | 2 | EA | 1.00 |
| 10 | 2 | EA | 1.00 |
| 14 | 2 | ml | 205.00 |
| 11 | 2 | ml | 25.00 |
| 6 | 3 | EA | 1.00 |
| 7 | 3 | EA | 1.00 |
| 11 | 3 | ml | 225.00 |
| 12 | 3 | EA | 1.00 |
| 9 | 4 | EA | 1.00 |
| 12 | 4 | EA | 1.00 |
| 12 | 5 | EA | 2.00 |
| 13 | 10 | g | 5.00 |
| 14 | 10 | ml | 20.00 |
| 14 | 12 | ml | 20.00 |
| 16 | 12 | g | 15.00 |
| 17 | 16 | g | 15.00 |

## 道路系统场景

我使用的道路系统场景指的是美国几个城市的道路系统，如图 11-4 所示。在此场景中，我选择了国际运输协会（IATA）代码来识别每个城市。

![](img/bdc38aa36f6e2987d913ee5381474711_739_0.png)

图 11-4 道路系统场景。

要创建 Cities 和 Roads 表并填充示例数据，请运行列表 11-3 中的代码。Cities 和 Roads 表的内容如表 11-4 和 11-5 所示。

## 列表 11-3 Cities 和 Roads 表的定义语言和示例数据

```sql
IF OBJECT_ID(N'dbo.Roads', 'U') IS NOT NULL DROP TABLE dbo.Roads;
IF OBJECT_ID(N'dbo.Cities', 'U') IS NOT NULL DROP TABLE dbo.Cities;
GO
CREATE TABLE dbo.Cities
(
  cityid CHAR(3) NOT NULL CONSTRAINT PK_Cities PRIMARY KEY,
  city VARCHAR(25) NOT NULL,
  region CHAR(2) NOT NULL,
  country CHAR(3) NOT NULL
);

INSERT INTO dbo.Cities(cityid, city, region, country) VALUES
('ATL', 'Atlanta', 'GA', 'USA'),
('DEN', 'Denver', 'CO', 'USA'),
('IAH', 'Houston', 'TX', 'USA'),
('LAX', 'Los Angeles', 'CA', 'USA'),
('MCI', 'Kansas City', 'MO', 'USA'),
('MIA', 'Miami', 'FL', 'USA'),
('MSP', 'Minneapolis', 'MN', 'USA'),
('JFK', 'New York', 'NY', 'USA'),
('SEA', 'Seattle', 'WA', 'USA'),
('SFO', 'San Francisco', 'CA', 'USA'),
('ANC', 'Anchorage', 'AK', 'USA'),
('FAI', 'Fairbanks', 'AK', 'USA');

CREATE TABLE dbo.Roads
(
  city1 CHAR(3) NOT NULL CONSTRAINT FK_Roads_city1 REFERENCES dbo.Cities,
  city2 CHAR(3) NOT NULL CONSTRAINT FK_Roads_city2 REFERENCES dbo.Cities,
  distance INT NOT NULL,
  CONSTRAINT PK_Roads PRIMARY KEY(city1, city2),
  CONSTRAINT CHK_Roads_citydiff CHECK(city1 < city2),
  CONSTRAINT CHK_Roads_posidist CHECK(distance > 0)
);

INSERT INTO dbo.Roads(city1, city2, distance) VALUES
('ANC', 'FAI', 359),
('ATL', 'ORD', 715),
('ATL', 'IAH', 800),
('ATL', 'MCI', 803),
('ATL', 'MIA', 665),
('ATL', 'JFK', 865),
('DEN', 'IAH', 1120),
('DEN', 'MCI', 600),
('DEN', 'LAX', 1025),
('DEN', 'MSP', 915),
('DEN', 'SEA', 1335),
('DEN', 'SFO', 1270),
('IAH', 'MCI', 795),
('IAH', 'LAX', 1550),
('IAH', 'MIA', 1190),
('JFK', 'ORD', 793),
('LAX', 'SFO', 385),
('MCI', 'ORD', 525),
('MCI', 'MSP', 440),
('MSP', 'ORD', 410),
('MSP', 'SEA', 2015),
('SEA', 'SFO', 815);
```

## 表 11-4 Cities 表的内容

| cityid | city | region | country |
|---|---|---|---|
| ANC | Anchorage | AK | USA |
| ATL | Atlanta | GA | USA |
| DEN | Denver | CO | USA |
| FAI | Fairbanks | AK | USA |
| IAH | Houston | TX | USA |
| JFK | New York | NY | USA |
| LAX | Los Angeles | CA | USA |
| MCI | Kansas City | MO | USA |
| MIA | Miami | FL | USA |
| MSP | Minneapolis | MN | USA |
| SEA | Seattle | WA | USA |
| SFO | San Francisco | CA | USA |

## 表 11-5 Roads 表的内容

| city1 | city2 | distance |
|---|---|---|
| ANC | FAI | 359 |
| ATL | ORD | 715 |
| ATL | IAH | 800 |
| ATL | MCI | 803 |
| ATL | MIA | 665 |
| ATL | JFK | 865 |
| DEN | IAH | 1120 |
| DEN | MCI | 600 |
| DEN | LAX | 1025 |
| DEN | MSP | 915 |
| DEN | SEA | 1335 |
| DEN | SFO | 1270 |
| IAH | MCI | 795 |
| IAH | LAX | 1550 |
| IAH | MIA | 1190 |
| JFK | ORD | 793 |
| LAX | SFO | 385 |
| MCI | ORD | 525 |
| MCI | MSP | 440 |
| MSP | ORD | 410 |
| MSP | SEA | 2015 |
| SEA | SFO | 815 |
