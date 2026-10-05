```
}

$query = "DROP TABLE buys";

$result = $connection->query($query);
if (DB::isError($result)) {
die("Could not inquiry the database: <br/>". $query.
".DB::errorMessage($result));\n}

echo "Table dropped effectively!";

$connection->disconnect();

?>
```

That worked incredibly, however you're going to require the buys table, so how about we reproduce the table by calling the create_table.php code in Example 13-1. Since you're modifying objects, there's a probability that the database won't give you a chance to do what you request that it do, which is the place lapses can happen. Dropping tables dangers information misfortune. Be extremely cautious about utilizing DROP!

# Lapses Happen

To verify you handle a lapse legitimately such as a grammatical error in the CREATE statement then again, for this situation, attempting to make a table that as now exists—execute the create_table. php script once more.

Expecting that your object was made without a lapse, you're going to need to control and add information to it from PHP. Hence, next you'll add information to a current table in light of information from the client.