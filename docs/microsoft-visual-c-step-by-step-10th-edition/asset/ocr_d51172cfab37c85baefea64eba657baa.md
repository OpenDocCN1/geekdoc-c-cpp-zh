```
public async Task<ActionResult<IEnumerable<CustomerModel>>> FindCustomers(
    string title = "%", string firstName = "%", string lastName = "%",
    string email = "%", string phone = "%"\)
{
    var query = from c in _context.Customers
        where EF.Functions.Like(c.Title, title) &&
        EF.Functions.Like(c.FirstName, firstName) &&
        EF.Functions.Like(c.LastName, lastName) &&
        EF.Functions.Like(c.EmailAddress, email) &&
        EF.Functions.Like(c.Phone, phone)
        select c;

    return await query.ToListAsync();
}
```