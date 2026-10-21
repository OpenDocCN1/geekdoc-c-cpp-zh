

## 理解 Recordset

你可以查看 Application 向导分段生成的 CProductSet 类的定义，并了解每个部分的工作原理。我将在代码片段中用阴影标出正在讨论的部分。

## Recordset 创建

类定义中感兴趣的第一段是：

```
class CProductSet : public CRecordset
{
public:
    CProductSet(CDatabase* pDatabase = NULL);
    DECLARE_DYNAMIC(CProductSet)
```

```
// Plus more of the class definition...
```

```
// Overrides
// Wizard generated virtual function overrides
public:
virtual CString GetDefaultConnect();    // Default connection string
```

```
virtual CString GetDefaultSQL();    // default SQL for Recordset
virtual void DoFieldExchange(CFieldExchange* pFX);// RFX support
```

```
// Plus some more standard stuff
```

```
};
```

该类以 CRecordset 为基类，并提供了从数据库检索数据的功能。类的构造函数接受一个指向 CDatabase 对象的指针，其默认值为 NULL。构造函数中的参数允许为已存在的 CDatabase 对象创建 CProductSet 对象，从而允许重用对数据库的现有连接。打开数据库连接是一项耗时的操作，因此在可能的情况下重用数据库连接是有利的。

如果未向构造函数传递指针，如文档类 CDBSampleDoc 的 m_DBsampleSet 成员的情况，框架会自动为你创建一个 CDatabase 对象，并调用 CProductSet 的 GetDefaultConnect() 成员函数来定义连接。Application 向导为此函数提供的实现如下：

```
CString CProductSet::GetDefaultConnect()
{
    return _T(
"DSN=Northwind;
DBQ=D:\Beg Visual C++ 2005\Model Access DB\Northwind.mdb;
DriverId=25;
FIL=MS Access;
MaxBufferSize=2048;
PageTimeout=5;
UID=admin;");
}
```

## 第 19 章

GetDefaultConnect() 函数是基类 CRecordset 中的纯虚函数，因此必须始终在派生的 recordset 类中实现。从函数返回的值是一个用双引号括起来的单个字符串，但我将其分散在多行中以使字符串的内容更清晰。Application 向导提供的实现将所示文本字符串返回给框架。这通过其名称和路径标识数据库，并为你可以看到的其他参数提供值，从而使框架能够创建一个 CDatabase 对象以自动建立数据库连接。连接字符串中参数的含义如下：

| Argument | Description |
|---|---|
| DSN | 数据源名称。 |
| DBQ | 数据库限定符，在本例中为 Access 数据库文件的路径。 |
| DriverID | 数据库 ODBC 驱动程序的 ID。 |
| FIL | 数据库文件类型。 |
| MaxBufferSize | 用于数据传输的缓冲区的最大大小。 |
| PageTimeout | 等待数据库连接的时间长度（秒）。将此值设置为足够的值很重要，以避免在访问远程数据库时连接失败。 |
| UID | 访问数据库的用户 ID。 |

实际上，在允许访问数据库之前，通常需要提供密码以及用户 ID，而且不建议以明文形式在代码中暴露密码。因此，Application 向导在 GetDefaultConnect() 函数的定义之前插入了以下行：

```
#error Security Issue: The connection string may contain a password
```

代码中存在此指令时编译会失败，因此你必须将其注释掉或删除才能成功编译程序。

你可以通过将 GetDefaultConnect() 函数中的 return 语句写成如下形式，使框架弹出对话框供用户从已注册的数据源列表中选择数据库名称：

```
return _T("ODBC;");
```

当需要访问数据库时，你还将被提示输入用户 ID 和密码。

## 查询数据库

CProductSet 类为 Products 表中的每个字段包含一个数据成员。Application 向导从数据库获取字段名称，并用这些名称命名类的相应数据成员。它们出现在 CProductSet 类定义中 Field/Param Data 注释之后的 code 块中：

### 连接到数据源

```cpp
class CProductSet : public CRecordset
{
public:
	CProductSet(CDatabase* pDatabase = NULL);
	DECLARE_DYNAMIC(CProductSet)

	// Field/Param Data
	// The string types below (if present) reflect the actual data type of the
	// database field - CStringA for ANSI datatypes and CStringW for Unicode
	// datatypes. This is to prevent the ODBC driver from performing
	// potentially unnecessary conversions.
	// If you wish, you may change these members to
	// Cstring types and the ODBC driver will perform all necessary
	// conversions.
	// (Note: You must use an ODBC driver version that is version 3.5 or
	// greater to support both Unicode and these conversions).

	long m_ProductID; // Number automatically assigned to new product.
	CStringW m_ProductName;
	long m_SupplierID; // Same entry as in Suppliers table.
	long m_CategoryID; // Same entry as in Categories table.
	CStringW m_QuantityPerUnit; // (e.g., 24-count case, 1-liter bottle).
	double m_UnitPrice;
	int m_UnitsInStock;
	int m_UnitsOnOrder;
	int m_ReorderLevel; // Minimum units to maintain in stock.
	BOOL m_Discontinued; // Yes means item is no longer available.

	// Overrides
	// Wizard generated virtual function overrides
	public:
	virtual CString GetDefaultConnect(); // Default connection string

	virtual CString GetDefaultSQL(); // default SQL for Recordset
	virtual void DoFieldExchange(CFieldExchange* pFX); // RFX support

	// Implementation
	#ifdef _DEBUG
	virtual void AssertValid() const;
	virtual void Dump(CDumpContext& dc) const;
	#endif

};
```

每个数据成员的类型设置为与 Products 表中相应字段的字段类型相对应。实际上你可能并不需要所有这些字段，但不应在类定义中随意删除它们。正如你很快就会看到的，它们在其他地方被引用，因此你必须确保删除对该字段的所有引用。另一个需要注意的是，你不得删除主键。如果这样做，recordset 将无法工作，因此在删除不需要的内容之前，你需要确定哪些字段是主键。

请注意，其中两个字段的类型为 CstringW。你以前没有见过它，但 CstringW 类类型只是封装了一个 Unicode 字符串而不是 ASCII 字符串。当

### 第 19 章

访问字段时使用类型 CString 会更方便，因此将 m_ProductName 和 m_QuantityPerUnit 成员的类型更改为 CString。这允许在示例中将字符串作为 ASCII 字符串处理。显然，如果你正在编写国际化数据库应用程序，则需要保持 CStringW 字段不变，因为它们可能包含不在 ASCII 字符集内的字符。

应用于 recordset 以填充这些数据成员的 SQL 操作在 GetDefaultSQL() 函数中指定。Application 向导为此提供的实现是：

```
CString CProductSet::GetDefaultSQL()
{
	return _T("Products");
}
```

返回的字符串显然是基于你在创建项目期间选择的表创建的。已包含方括号以提供表名可能包含空格的可能性。如果你曾在项目创建过程中选择了多个表，它们都将被插入此处，以逗号分隔，每个表名都用方括号括起来。

当 MFC 框架构造要应用于 recordset 的 SQL 语句时，会调用 GetDefaultSQL() 函数。框架将此函数返回的字符串插入到形式为的骨架 SQL 语句中：

> SELECT * FROM < String returned by GetDefaultSQL() >;

这看起来很简单，实际上也是如此，但你可以添加 WHERE 和 ORDER BY 子句到操作中，如你稍后会看到的。

从数据库到 recordset 以及反向的数据传输由 CProductSet 类的 DoFieldExchange() 成员完成。此函数的实现是：

```
void CProductSet::DoFieldExchange(CFieldExchange* pFX)
{
	pFX->SetFieldType(CFieldExchange::outputColumn);
	// Macros such as RFX_Text() and RFX_Int() are dependent on the
	// type of the member variable, not the type of the field in the database.
	// ODBC will try to automatically convert the column value to the requested
	// type
	RFX_Long(pFX, _T("[ProductID]"), m_ProductID);
	RFX_Text(pFX, _T("[ProductName]"), m_ProductName);
	RFX_Long(pFX, _T("[SupplierID]"), m_SupplierID);
	RFX_Long(pFX, _T("[CategoryID]"), m_CategoryID);
	RFX_Text(pFX, _T("[QuantityPerUnit]"), m_QuantityPerUnit);
	RFX_Double(pFX, _T("[UnitPrice]"), m_UnitPrice);
	RFX_Int(pFX, _T("[UnitsInStock]"), m_UnitsInStock);
	RFX_Int(pFX, _T("[UnitsOnOrder]"), m_UnitsOnOrder);
	RFX_Int(pFX, _T("[ReorderLevel]"), m_ReorderLevel);
	RFX_Bool(pFX, _T("[Discontinued]"), m_Discontinued);
}
```

