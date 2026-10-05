# # 13.9 Interim Recap

Because there can be so much confusion with namespace, using, and static, I will recapitulate the various usage scenarios here. For completeness, I will also include the type alias with using.

| Language Element | Description |
|---|---|
| namespace xyz {...} | New namespace xyz |
| namespace {...} | Anonymous namespace; all identifiers file-local |
| inline namespace XYZ {...} | Embedded namespace |
| static global variable | File-local variable |
| static free function | File-local function |
| static data field | Shared between all instances of the class |
| static method | Method that you call without specific instance |
| static local variable | A variable that persists beyond the scope |
| using namespace xyz | Import all identifiers from namespace xyz |