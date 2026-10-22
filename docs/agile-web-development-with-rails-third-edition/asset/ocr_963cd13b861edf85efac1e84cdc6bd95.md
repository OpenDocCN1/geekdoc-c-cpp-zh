# Loading Data from Fixtures

Fixtures normally contain data to be used when running tests. However, with a little extra plumbing, we can also use them to load data during a migration.

To illustrate the process, let's assume our database has a new users table.

Let's create a subdirectory under db/migrate to hold the data we'll be loading into our development database. Let's call that directory dev_data:

```
depots> mkdir db/migrate/dev_data
```

In that directory, we'll create a YAML file containing the data we want to load into our users table. We'll call that file users.yml:

```
dave:
  name: Dave Thomas
  status: admin

mike:
  name: Mike Clark
  status: admin

fred:
  name: Fred Smith
  status: audit
```

Now we'll generate a migration to load the data from this fixture into our development database:

```
depots> ruby script/generate migration load_users_data
exists  db/migrate
create  db/migrate/20080601000020_load_users_data.rb
```

And finally we'll write the code in the migration that loads data from the fixture. This is slightly magical, because it relies on a backdoor interface into the Rails fixture code.

```
require 'active_record/fixtures'

class LoadUserData < ActiveRecord::Migration
  def self.up
    directory = File.join(File.dirname(__FILE__), 'dev_data')
    Fixtures.create_fixtures(directory, "users")
  end

  def self.down
    User.delete_all
  end
end
```