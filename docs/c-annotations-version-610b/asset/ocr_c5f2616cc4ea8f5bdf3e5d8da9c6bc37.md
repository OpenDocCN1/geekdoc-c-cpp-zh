```
TableType::TableType(TableSupport &tableSupport, size_t nColumns,
                      FillDirection direction)
:
    d_tableSupportPtr(0),
    d_tableSupport(tableSupport),
    d_maxWidth(0),
    d_nRows(0),
    d_nColumns(nColumns),
    d_widthType(COLUMNWIDTH),
    d_colWidth(nColumns),
    d_widthFn(&TableType::columnWidth),
    d_indexFun(direction == HORIZONTAL ?
                   &TableType::hIndex
               :
                   &TableType::vIndex)
{}
```

+   - Once `d_string` has been filled, the table is initialized by `Table::fill`. The init protected member resizes `d_string` so that its size is exactly rows × columns, and it determines the maximum width of the elements per column. Its implementation is straightforward:

```
#include "tabletype.h"

void TableType::init()
{
    if (!d_string.size())                         // no elements
        return;                                   // then do nothing

    d_nRows = (d_string.size() + d_nColumns - 1) / d_nColumns;
    d_string.resize(d_nRows * d_nColumns);       // enforce complete table

                                                  // determine max width per column,
                                                  // and max column width
    for (size_t col = 0; col < d_nColumns; col++)
    {
        size_t width = 0;
        for (size_t row = 0; row < d_nRows; row++)
        {
            size_t len = stringAt(row, col).length();
            if (width < len)
                width = len;
        }
        d_colWidth[col] = width;

        if (d_maxWidth < width)                 // max. width so far.
            d_maxWidth = width;
    }
}
```

+   - The public member `insert` is used by the insertion operator (`operator<<`) to insert a Table into a stream. First it informs the TableSupport object about the table’s dimensions. Next it displays the table, allowing the TableSupport object to write headers, footers and separators:

```
#include "tabletype.h"

ostream &TableType::insert(ostream &ostr) const
{
    if (!d_nRows)
        return ostr;
```