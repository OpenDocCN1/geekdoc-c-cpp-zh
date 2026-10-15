| Selection statements | if (condition) { // do something } |
| Iteration statements | foreach (item in list) { // do something } |
| Declaration statements | string greeting; |
| Expression statements | int sum = 50 + 50; |
| Exception statements | try { // risky code } catch { // fallback } |

Exception handling statements allow us to catch and address issues in our code. Again, statements are complete instructions that actually do things in the C# language, and there are additional options beyond these essential types listed here. You may have noticed already that statements can span one or many lines in your application.

```
public decimal GetSalesTax(product item)
{
    var price = item.Price;
    var salesTax = price * 1.06;
    return salesTax;
}
```