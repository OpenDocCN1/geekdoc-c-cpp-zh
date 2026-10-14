```
<ItemGroup>
    <Reference Include="System"/>
    $if$ ($targetframeworkversion$ >= 3.5)
    <Reference Include="System.Core"/>
    <Reference Include="System.Xml.Linq"/>
    <Reference Include="System.Data.DataSetExtensions"/>
    $endif$
    $if$ ($targetframeworkversion$ >= 4.0)
    <Reference Include="Microsoft.CSharp"/>
    $endif$
    <Reference Include="System.Data"/>
    <Reference Include="System.Xml"/>
</ItemGroup>
```