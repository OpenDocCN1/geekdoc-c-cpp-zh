```
create  app/views/articles/index.html.erb
create  app/views/articles/show.html.erb
create  app/views/articles/new.html.erb
create  app/views/articles/edit.html.erb
create  app/views/layouts/articles.html.erb
create  public/stylesheets/scaffold.css
create  app/controllers/articles_controller.rb
create  test/functional/articles_controller_test.rb
create  app/helpers/articles_helper.rb
    route  map.resources :articles
dependency  model
exists     app/models/
exists     test/unit/
exists     test/fixtures/
create     app/models/article.rb
create     test/unit/article_test.rb
create     test/fixtures/articles.yml
create     db/migrate
create     db/migrate/20080601000001_create_articles.rb
```

Take a look at the line that starts with route in the output of this command. It’s telling us that the generator has automatically added the appropriate mapping to our application’s routes. Let’s take a look at what it did. Look at the top of the file routes.rb in the config/ directory:

```
Download restful/config/routes.rb
ActionController::Routing::Routes.draw do |map|
  map.resources :articles
  # ...
  map.connect ':controller/:action/:id'
  map.connect ':controller/:action/:id.:format'
end
```

The migration file was automatically created and populated with the information we gave the generator:

```
Download restful/db/migrate/20080601000001_create_articles.rb
class CreateArticles < ActiveRecord::Migration
  def self.up
    create_table :articles do |t|
      t.string :title
      t.text :summary
      t.text :content
      t.timestamps
    end
  end
  def self.down
    drop_table :articles
  end
end
```