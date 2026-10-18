
第 [12, 15] 行定义了 `Online_CurExchanger` 命名空间内局部使用的 `wstring` 对象。它们只是保存了 XML“来源”文件和“目标”文件的互联网地址与本地默认地址。正如已经指出的，下载的 XML 文件提供了对当前汇率数据的访问。此外，如果有必要，这两个地址可以很方便地访问和修改。在第 [18] 行，通过定义局部变量 `kMyOS` 来指明我们所用的操作系统。

`CurExchanger_DownloadCurrencies` 函数定义在第 [19–23] 行。它的作用是创建一个名为 `http_client` 的 `HTTP_File_Handle` 对象，并在所选平台上对其进行适当初始化。随后，该对象被用来从互联网位置下载 XML 文件并保存到本地。

```cpp
bool CurExchanger_DownloadCurrencies(    const wstring & http_addr,
                                         const wstring & local_XML_FullPath )
{
    HTTP_File_Handle http_client( kMyOS );
    return http_client.Load_HTTP_File( nb_addr, local_XML_FullPath );
}
```

接下来，我们会看到，下载的 XML 文件会被用来初始化 `XML_CurrencyExchanger`。但在此时，明智的做法是将当前货币数据保存到一个单独的初始化文件中。这样可以在例如没有互联网连接、无法下载 XML 文件的情况下使用。这一功能由第 [24] 行定义的 `CurExchanger_SaveInitFile` 函数完成。

```cpp
void CurExchanger_SaveInitFile(      const XML_CurrencyExchanger & obj,
                                      const wstring & initFileFullPath )
{
    // Save to the init file
    // Use default file to load currencies
    wofstream outFile( initFileFullPath );
    const XML_CurrencyExchanger::CurrencyMap & cur_map = obj.GetCurrencyMap();
    transform( cur_map.cbegin(), cur_map.cend(),
                ostream_iterator< TCurrency, wchar_t >( outFile, L"\n" ),
                []( const XML_CurrencyExchanger::CurrencyMap::value_type & vt )
                { return vt.second; } );
}
```

在上一段代码中，第 [30–32] 行的 `std::transform` 函数需要一些解释（另见表 3.6）。正如我们已经知道的，`std::map` 对象的每个元素都包含 `key` 和 `value` 两部分。`std::transform` 的作用是把 `CurrencyMap` 中每个元素的 `value` 部分复制到由 `outFile` 对象标识的输出文件中。这个 `CurrencyMap` 对象通过局部引用 `cur_map` 访问。要复制的范围由前两个参数传入，即 `cur_map.cbegin()` 和 `cur_map.cend()`。它们返回指向该 map 集合开头和末尾的常迭代器（这里以字母 c 开头）。输出通过 `ostream_iterator` 写入 `outFile`，该迭代器在第 [31] 行设置为处理 `TCurrency` 和宽字符。每个货币条目都是通过在第 3.33 节清单 3.33 中第 [7–26] 行讨论过的对 `operator <<` 的自动调用来保存的。每个这样的条目由提供给 `ostream_iterator` 的宽换行符号 `L"\n"` 分隔。最后但同样重要的是第 [32] 行提供的 lambda 函数，它是 `std::transform` 的最后一个参数。它由 `std::transform` 内部调用，传入 `vt` 引用以引用 `cur_map` 的连续元素。这个 lambda 的作用很简单：跳过 `key`，只返回元素由 `vt.second` 标识的 `value` 部分。

`CreateCurExchanger` 函数的定义从第 [40] 行开始。它与 3.18.5 节中介绍的同名函数类似。但两者返回的对象类型不同，本例中返回的是 `XML_CurrencyExchanger` 而不是 `CurrencyExchanger`。此外，它们的初始化方式也不同，本例中是通过

[PAGE 418]

从互联网下载的 XML 文件进行初始化。不过，和之前一样，由于对象创建过程可能失败，`CreateCurExchanger` 返回一个在第 [34] 行定义的 `std::optional` 对象。如果对象创建成功，它允许我们传递一个有效对象；如果由于某种原因无法提供对象，它就是空的。

```cpp
using XML_CurrExch_Optional = std::optional< XML_CurrencyExchanger >;

// There are two options for the return object:
// - It is either TCurrencyExchanger if properly built
// - or empty CurrExch_Optional if cannot create
auto CreateCurExchanger( const wstring & http_XML_FileName,
const wstring & initFileFullPath )
{
XML_CurrencyExchanger currencyExchangerObj;
namespace fs = std::filesystem;
// Create name of a local XML file - its parent is from initFileFullPath
wstring local_xml_full_path( fs::path( initFileFullPath ).parent_path()
/ local_xml:file_name );

if( CurExchanger_DownloadCurrencies( http_XML_FileName, local_xml_full_path )
== true &&
currencyExchangerObj.FillCurrencyTableFrom( local_xml_full_path )
== true )
{
// Success, object initialized from Internet
// Add the reference currency (PLN) (0xB3 is Polish letter "l-crossed")
currencyExchangerObj.AddCurrency( { L"PLN", L"z\\xB3oty-polski",1,0,1.0 });
// Update the ini file with new data
CurExchanger_SaveInitFile( currencyExchangerObj, initFileFullPath );
}
else
{
// Cannot initialize from the Internet,
// so, as a last resort, let's look for a local ini file
wifstream inFile( initFileFullPath );
if( inFile.is_open() == false )
return XML_CurrExch_Optional(); // no ini file, return empty optional
// Read data from the file
inFile >> currencyExchangerObj;
}
return XML_CurrExch_Optional( currencyExchangerObj );
}
```

传递给 `CreateCurExchanger` 的两个参数是 `http_XML_FileName`（保存着包含当前汇率数据的 XML 文件的互联网地址）和 `initFileFullPath`（保存着本地初始化文件的完整路径）。该路径在第 [47] 行用来创建另一个本地文件的名称——即存储下载所得 XML 文件的那个文件。这些文件，即初始化文件和本地 XML 文件，都包含货币数据，但格式不同。为了创建新路径，我们使用了文件系统路径对象及其 `parent_path`，以及重载的 `/`（斜杠）运算符，如表 6.3 所示。

[PAGE 419]

在第 [49, 50] 行，使用 `_CurExchanger_\_DownloadCurrencies_` 函数下载 XML 文件。当且仅当此操作成功时，才会使用该 XML 文件通过调用 `_FillCurrencyTableFrom_` 成员来初始化货币 `_ExchangerObj_` 对象。如果文件下载失败，由于逻辑表达式的求值顺序（见第 3.19.2 节），`_FillCurrencyTableFrom_` 不会被调用。如果这两个步骤都成功，那么在第 [55] 行添加参考货币（本例中为波兰兹罗提）。接下来，在第 [58] 行保存新版本的初始化文件。这在将来无法从互联网下载时可以使用。最后，在第 [60] 行，该分支返回一个有效对象：在第 [42] 行创建的局部 `currencyExchangerObj` 对象的副本。
如果互联网下载失败，那么在第 [67] 行，我们尝试使用本地初始化文件来初始化 `_currencyExchangerObj_` 对象。如果这样的文件无法打开，那么我们在第 [68] 行通过返回一个空对象来表示这种情况：第 [68] 行的 _optional_ 对象。假设初始化文件可用，则在第 [71] 行使用它来读取货币数据。这完全类似于先前版本的 `CreateCurExchanger` 函数（第 3.18.5 节）。然后，在第 [74] 行返回一个有效的 `XML_CurrencyExchanger` 对象：在第 [42] 行创建的局部 `currencyExchangerObj` 对象的副本。
在第 [77] 行，定义了新版本的 `Run` 函数。在第 [84] 行，调用 `CreateCurExchanger` 函数，它返回 `XML_CurrencyExchanger` 对象。然而，在第 [87] 行，调用的是我们在第 3.18.5 节中定义的 `CurrExchanger::Run` 函数。有趣的是，它接收到的是新的 `XML_CurrencyExchanger` 类型的对象，而这个版本的 `Run` 原本定义为接受 `TCurrencyExchanger` 对象的常量引用。在面向对象框架中，这是可以的，因为派生类的对象可以在任何使用其基类对象的地方使用。这是多态性和里氏替换规则的示例，将在第 4.1 节中讨论。还要注意，这个“旧”版本的 `Run` 会调用其他“旧”函数，例如 `DisplayAllCurrencies` 和 `UserInterface`。这些函数也可以处理这个新版本的传入对象。

```cpp
// All actions
void Run( void )
{
    namespace fs = std::filesystem;
    wstring iniPath (fs::current_path() / fs::path( initDefaultFileName ));;
    // First try to get the currency object
    if( XML_CurrExch_Optional all_my_options
    { CreateCurExchanger(nbp_addr, iniPath ); all_my_options )
    { // Functions do not overload over namespaces
    CurrExchanger::Run( * all_my_options ); // so we have to use CurrExchanger::
    } else
    { wcout << L"Error, check Currency.txt file." << endl
    << L"Exiting ..." << endl;
    }
}
```


