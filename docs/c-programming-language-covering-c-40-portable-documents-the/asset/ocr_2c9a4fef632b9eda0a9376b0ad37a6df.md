```
enum-modifier:
new
public
protected
internal
private
```

```
enum-member-declarations:
enum-member-declaration
enum-member-declarations , enum-member-declaration
```

```
enum-member-declaration:
    attributes_opt identifier
    attributes_opt identifier = constant-expression
```

# B.2.12 Delegates

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
        ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;
```

```
delegate-modifiers:
    delegate-modifier
    delegate-modifiers delegate-modifier
```

```
delegate-modifier:
new
public
protected
internal
private
```

# B.2.13 Attributes

```
global-attributes:
    global-attribute-sections

global-attribute-sections:
    global-attribute-section
    global-attribute-sections global-attribute-section

global-attribute-section:
    [ global-attribute-target-specifier attribute-list ]
    [ global-attribute-target-specifier attribute-list , ]
```