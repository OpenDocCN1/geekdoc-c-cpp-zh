name/user identifier pair doesn't have any null values.

Let's use the syntax to create a role:

```
CREATE ROLE READERS;
```

That's it. After creating this role, you will be able to grant it to users or other roles.

To drop (or delete) a role, you just have to use the following syntax:

```
DROP ROLE (name of role)
```

This syntax has a single requirement: the name of the role you want to delete.