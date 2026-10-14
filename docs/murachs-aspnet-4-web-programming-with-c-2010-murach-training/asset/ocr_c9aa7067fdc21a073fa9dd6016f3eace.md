# The DataSourceMode attribute

| Attribute | Description |
|---|---|
| DataSourceMode | DataSet or DataReader. The default is DataSet, but you can specify DataReader if the data source is read-only. |

# A SqlDataSource control that uses a data reader

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConnectionString="<%= ConnectionStrings:HalloweenConnectionString %>"
    DataSourceMode="DataReader"
    SelectCommand="SELECT [CategoryID], [LongName]
        FROM [Categories]
        ORDER BY [LongName]"
</asp:SqlDataSource>
```

# SqlDataSource attributes for caching

| Attribute | Description |
|---|---|
| EnableCaching | A Boolean value that indicates whether caching is enabled for the data source. The default is False. |
| CacheDuration | The length of time in seconds that the cached data should be saved in cache storage. |
| CacheExpirationPolicy | If this attribute is set to Absolute, the cache duration timer is started the first time the data is retrieved and is not reset to zero until after the time has expired. If this attribute is set to Sliding, the cache duration timer is reset to zero each time the data is retrieved. The default is Absolute. |
| CacheKeyDependency | A string that provides a key value associated with the cached data. If you provide a key for the cached data, you can use the key value to programmatically expire the cached data at any time. |

# A SqlDataSource control that uses caching

```
<asp:SqlDataSource ID="SqlDataSource1" runat="server"
    ConnectionString="<%= ConnectionStrings:HalloweenConnectionString %>"
    EnableCaching="True" CacheDuration="60"
    SelectCommand="SELECT [CategoryID], [LongName]
        FROM [Categories]
        ORDER BY [LongName]"
</asp:SqlDataSource>
```

# Description

+   - The DataSourceMode attribute lets you specify that data should be retrieved using a data reader rather than being stored in a dataset. For read-only data, a data reader is usually more efficient.
+   - The data source caching attributes let you specify that data should be stored in cache storage for a specified period of time. For data that changes infrequently, caching can improve performance.