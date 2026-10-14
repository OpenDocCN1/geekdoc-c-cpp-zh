```
private MongoDatabase GetDatabase()
{
    var connectionString = applicationSettings.GetValue(MongoConnectionString);
    var client = new MongoClient(connectionString);
    var server = client.GetServer();
    return server.GetDatabase(ProsewareDatabase);
}

private readonly IApplicationSettings applicationSettings;
private static string MongoConnectionString = "MongoConnectionString";
private static string ProsewareDatabase = "Proseware";
private static string MessagesCollection = "messages";
private static string RoomsCollection = "rooms";
}
```