highest version number and applies its undo action. This removes the migration’s change from the schema and from the schema_migrations table. It repeats this process until the database reaches the desired version.

# 17.1 Creating and Running Migrations

A migration is simply a Ruby source file in your application’s db/migrate directory. Each migration file’s name starts with a number of digits (typically fourteen) and an underscore. Those digits are the key to migrations, because they define the sequence in which the migrations are applied—they are the individual migration’s version number.

Here’s what the db/migrate directory of our Depot application looks like:

```
depot> ls db/migrate
20080601000001_create_products.rb
20080601000002_add_price_to_product.rb
20080601000003_add_test_data.rb
20080601000004_create_sessions.rb
20080601000005_create_orders.rb
20080601000006_create_line_items.rb
```

Although you could create these migration files by hand, it’s easier (and less error prone) to use a generator. As we saw when we created the Depot application, there are actually two generators that create migration files:

+   - The *model* generator creates a migration to in turn create the table associated with the model (unless you specify the `--skip-migration` option). As the example that follows shows, creating a model called discount also creates a migration called `dddddddddddddd_create_discounts.rb`:
+   
+     ```text
+     depot> ruby script/generate model discount
+          exists  app/models/
+          exists  test/unit/
+          exists  test/fixtures/
+          create  app/models/discount.rb
+          create  test/unit/discount_test.rb
+          create  test/fixtures/discounts.yml
+          exists  db/migrate
+          create  db/migrate/20080601000014_create_discounts.rb
+     ```

+   - You can also generate a migration on its own:
+   
+     ```text
+     depot> ruby script/generate migration add_price_column
+          exists  db/migrate
+          create  db/migrate/20080601000015_add_price_column.rb
+     ```

Later, starting in *Anatomy of a Migration*, we’ll see what goes in the migration files. But for now, let’s jump ahead a little in the workflow and see how to run migrations.