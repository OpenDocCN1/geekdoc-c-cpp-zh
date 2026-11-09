```
```csharp
// NOTE: This line may be deleted if you trust
// that the base type implemented Equals correctly.
if (obj == null) return false;

// If the objects are of different types, they can't be equal
// NOTE: This line may be deleted if you trust
// that the base type implemented Equals correctly.
if (this.GetType() != obj.GetType()) return false;

// Cast obj to our type to access fields. NOTE: This cast
// can't fail since we know objects are of the same type
AccountsAttribute other = (AccountsAttribute) obj;

// Compare the fields to see if they have the same value
// This example checks if 'this' accounts is the same
// as other's accounts
if (other.m_accounts != m_accounts)
    return false;

return true;    // Objects are equal
}

// Override GetHashCode since we override Equals
public override Int32 GetHashCode() {
    return (Int32) m_accounts;
}

[Accounts(Accounts.Savings)]
internal sealed class ChildAccount { }

[Accounts(Accounts.Savings | Accounts.Checking | Accounts.Brokerage)]
internal sealed class AdultAccount { }

public sealed class Program {
    public static void Main() {
        CanWriteCheck(new ChildAccount());
        CanWriteCheck(new AdultAccount());

        // This just demonstrates that the method works correctly on a
        // type that doesn't have the AccountsAttribute applied to it.
        CanWriteCheck(new Program());
    }

    private static void CanWriteCheck(Object obj) {
        // Construct an instance of the attribute type and initialize it
        // to what we are explicitly looking for.
        Attribute checking = new AccountsAttribute(Accounts.Checking);

        // Construct the attribute instance that was applied to the type
```
```