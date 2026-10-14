```
public AccountService(IAccountRepository repository)
{
    if (repository == null) throw new ArgumentNullException("repository", "A valid account repository must be supplied.");

    this.repository = repository;
}
```