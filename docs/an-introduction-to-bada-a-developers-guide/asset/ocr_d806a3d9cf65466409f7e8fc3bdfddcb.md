# Hints, Pitfalls, and Related Topics

In Example 1 of this recipe, the `CreateDateTimeFormatterN()`, `Create-DateFormatterN()` and `CreateTimeFormatterN()` methods are used to create date/time formatters. These methods have an ‘N’ postfix, so to prevent memory leaks the caller must delete the returned instance after the caller is finished with the instance.

# Related Recipe

+   - Add a Form to a Frame-based App