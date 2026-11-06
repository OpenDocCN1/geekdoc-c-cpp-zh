In our example, the purpose is to manipulate copy counters. Therefore, our data are integers and the pointers have type int*. We know that we will have exactly 100 pointers, one for each user. Therefore, we can choose an array

```
```
int* users[100];
```
```

# **Step 3**

Initialize the pointers with variable addresses or heap memory.

Will you allocate variables and then take their addresses with the & operator? That is fine if you have a fixed amount of data that you want to reach through the pointers. Otherwise, use the new operator to allocate memory dynamically. Be sure to deallocate the memory when you are done, using the delete or delete[] operator.

In our example, there is no need for dynamic allocation, so we will just take addresses of variables.

```
```
int master_account;
int project_accounts[10];
for (int i = 0; i < 100; i++)
{
    users[i] = &master_account;
}
// Here we reassign several users to project accounts.
// The following code is a simulation of the actions that would
// occur in an administration interface, which we do not implement.
users[2] = project_accounts + 1
users[3] = project_accounts + 2
users[99] = project_accounts + 2
```
```

# **Step 4**

Use the * or [] operator to access your data.

When you access a single variable through a pointer, use the * operator to read or write the variable. For example,

```
```
*account_pointer = *account_pointer + 20;
```
```

When you have a pointer to an array, use the [] notation. Simply think of the pointer as the array:

```
```
account_array[1] = account_array[1] + 20;
```
```

If you have an array or vector of pointers, then you need brackets to get at an individual pointer. Then supply another * or [] to get at the value. You saw an example in the Galton board simulator where a count was accessed as

```
```
counts[i][j]
```
```

Implement your algorithm, keeping these access rules in mind.

In our example, we read the user ID and number of copies. Then we increment the copy account:

```
```
cin >> id >> copies;
*users[id] = *users[id] + copies;
```
```

Exercise P7.12 asks you to complete this simulation.

# **WORKED EXAMPLE 7.1**   **Producing a Mass Mailing**

![](bbox=[0.109, 0.855, 0.25, 0.925])

This Worked Example uses pointers to create a template for a mass mailing