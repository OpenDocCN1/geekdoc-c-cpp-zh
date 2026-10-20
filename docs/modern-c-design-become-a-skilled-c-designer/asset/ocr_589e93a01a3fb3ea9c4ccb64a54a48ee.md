above, the entire interface for the CLI can be given by the code in Listing 5-4.

# Listing 5-4. The Entire Interface for the CLI

```
class Cli : public UserInterface
{
class CliImpl;
public:
Cli(istream& in, ostream& out);
~Cli();

void execute(bool suppressStartupMessage = false, bool echo = false);

private:
void postMessage(const string& m) override;
void stackChanged() override;

unique_ptr<CliImpl> pimpl_;
};
```

While the interface is mostly self-explanatory, the arguments to both the constructor and the execute() function are worth explaining. To meet the requirements