# Coding Common JavaScript Tasks

JavaScript can be used to perform many tasks, from simple variable assignments to complex data visualizations. The following tasks, here explained within a JavaScript context, are core programming concepts that haven’t changed in the last twenty years and won’t change in the next twenty. They’re applicable to any programming language. Finally, I’ve listed instructions on how to perform these tasks, but if you prefer you can also practice these skills right away by jumping ahead to the “Writing Your First JavaScript Program” section, later in this chapter.

# Storing data with variables

Variables, like those in algebra, are keywords used to store data values for later use. Though the data stored in a variable may change, the variable name remains the same. Think of a variable like a gym locker — what you store in the locker changes, but the locker number always stays the same. The variable name usually starts with a letter, and Table 9-1 lists some types of data JavaScript variables can store.

For a list of rules on variable names see the “JavaScript Variables” section at www.w3schools.com/js/js_variables.asp

![](bbox=[0.118, 0.456, 0.207, 0.526])

**Table 9-1: Data Stored by a Variable**

| Data Type | Description | Examples |
|---|---|---|
| Numbers | Positive or negative numbers with or without decimals | 156–101.96 |
| Strings | Printable characters | Holly<br>NovakSenior |
| Boolean | Value can either be true or false. | truefalse |

The first time you use a variable name, you use the word var to declare the variable name. You can optionally assign a value to variable using the equals sign. In the following code example, I declare three variables and assign values to those variables:

```
```javascript
var myName="Nik";
var pizzaCost=10;
var totalCost=pizzaCost * 2;
```
```