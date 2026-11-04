```
// Encrypt connection string
byte[] encryptedBytes = ProtectedData.Protect(Encoding.Unicode.GetBytes(connectionString), null, DataProtectionScope.CurrentUser);

// Decrypt connection string
byte[] decryptedBytes = ProtectedData.Unprotect(encryptedBytes, null, DataProtectionScope.CurrentUser);
string decryptedConnectionString = Encoding.Unicode.GetString(decryptedBytes);
```

# Storing Connection Strings Securely

Storing connection strings securely is crucial. Avoid storing them in plain text within application source code or configuration files. Instead, consider using Azure Key Vault or encrypted configuration providers:

```
// Using Azure Key Vault
AzureServiceTokenProvider azureServiceTokenProvider = new AzureServiceTokenProvider();
var keyVaultClient = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(azureServiceTokenProvider.KeyVaultTokenCallback));
SecretBundle secret = await keyVaultClient.GetSecretAsync("https://your-key-vault.vault.azure.net/secrets/your-secret-name");
string connectionString = secret.Value;
```

```
// Using encrypted configuration providers
var builder = new ConfigurationBuilder()
    .AddJsonFile("appsettings.json", optional: false, reloadOnChange: true)
    .AddEnvironmentVariables()
    .AddAzureKeyVault("https://your-key-vault.vault.azure.net/", new DefaultAzureCredential());

var configuration = builder.Build();
string connectionString = configuration.GetConnectionString("YourConnectionStringKey");
```

# Protecting Sensitive Data During Transmission

Ensure data is protected during transmission by using secure communication protocols like SSL/TLS:

```
using System.Data.SqlClient;
```