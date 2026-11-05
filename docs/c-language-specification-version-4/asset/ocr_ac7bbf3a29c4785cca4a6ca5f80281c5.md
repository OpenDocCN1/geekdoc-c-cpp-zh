```
```
<permission cref="member">description</permission>
```
```

where

`cref="member"`

The name of a member. The documentation generator checks that the given code element exists and translates *member* to the canonical element name in the documentation file.

*description*

A description of the access to the member.

**Example:**

```
```
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>
public static void Test() {
    // ...
}
```
```

# ### A.2.11 <remark>

This tag is used to specify extra information about a type. (Use <summary> ($A.2.15) to describe the type itself and the members of a type.)

**Syntax:**

```
```
<remark>description</remark>
```
```

where

*description*

The text of the remark.

**Example:**

```
```
/// <summary>Class <c>Point</c> models a point in a
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point
{
    // ...
}
```
```

# ### A.2.12 <returns>

This tag is used to describe the return value of a method.

**Syntax:**

```
```
<returns>description</returns>
```
```

where

*description*

A description of the return value.

**Example:**

```
```
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
/// without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```
```