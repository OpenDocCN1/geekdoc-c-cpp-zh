# Table 22.5: EDM Type Facets to Corresponding Provider Type Names

| Provider Type Name | EDM Type Name | EDM Type Facets |  |  |
|---|---|---|---|---|
| image: Supports the Equal Comparable and Order Comparable attributes when set to False | Binary | Facet Name | Attribute Name | Value |
|  |  | MaxLength | Default | 2147483647 |
|  |  |  | Constant | True |
|  |  | FixedLength | Default | False |
|  |  |  | Constant | True |
| timestamp: Supports the Equal Comparable and Order Comparable attributes when set to True | Binary | Facet Name | Attribute Name | Value |
|  |  | MaxLength | Default | 8 |
|  |  |  | Constant | True |
|  |  | FixedLength | Default | True |
|  |  |  | Constant | True |
| rowversion: Supports the Equal Comparable and Order Comparable attributes when set to True | Binary | Facet Name | Attribute Name | Value |
|  |  | MaxLength | Default | 8 |
|  |  |  | Constant | True |
|  |  | FixedLength | Default | True |
|  |  |  | Constant | True |
| smalldatetime: Supports the Equal Comparable and Order Comparable attributes when set to True | DateTime | Facet Name | Attribute Name | Value |
|  |  | PreserveSeconds | Default | False |
|  |  |  | Constant | True |
|  |  | DateTimeKind | Default | Unspecified |
|  |  |  | Constant | True |
| datetime: Supports the Equal Comparable and Order Comparable attributes when set to True | DateTime | Facet Name | Attribute Name | Value |
|  |  | PreserveSeconds | Default | True |
|  |  |  | Constant | True |
|  |  | DateTimeKind | Default | Unspecified |
|  |  |  | Constant | True |
| nvarchar: Supports the Equal Comparable and Order Comparable attributes when set to True | String | Facet Name | Attribute Name | Value |
|  |  | MaxLength | Minimum | 1 |
|  |  |  | Maximum | 4000 |
|  |  |  | Default | 4000 |
|  |  |  | Constant | False |
|  |  | Unicode | Default | True |
|  |  |  | Constant | True |
|  |  | FixedLength | Default | False |
|  |  |  | Constant | True |