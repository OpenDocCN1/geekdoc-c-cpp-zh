```
c = CatalogEntry.new(:name => 'Sound One', :acquired_at => Time.now)
c.resource = Sound.new(:content => "more binary data")
c.save!
```

Now our database looks more interesting:

```
depots> sqlite3 -line db/development.sqlite3 "select * from articles"
    id = 1
content = This is my new article

depots> sqlite3 -line db/development.sqlite3 "select * from images"
    id = 1
content = some binary data

depots> sqlite3 -line db/development.sqlite3 "select * from sounds"
    id = 1
content = more binary data

depots> sqlite3 -line db/development.sqlite3 "select * from catalog_entries"
    id = 2
    name = Article One
acquired_at = 2008-05-14 12:03:24
    resource_id = 2
resource_type = Article

    id = 3
    name = Image One
acquired_at = 2008-05-14 12:03:24
    resource_id = 1
resource_type = Image

    id = 4
    name = Sound One
acquired_at = 2008-05-14 12:03:24
    resource_id = 1
resource_type = Sound
```

Notice how all three foreign keys in the catalog have an id of 1—they are distinguished by their type column.

Now we can retrieve all three assets by iterating over the catalog:

```
Download e1/ar/polymorphic.rb
CatalogEntry.find(:all).each do |c|
  puts "#{c.name}: #{c.resource.class}"
end
```

This produces the following:

```
Article One:  Article
Image One:  Image
Sound One:  Sound
```