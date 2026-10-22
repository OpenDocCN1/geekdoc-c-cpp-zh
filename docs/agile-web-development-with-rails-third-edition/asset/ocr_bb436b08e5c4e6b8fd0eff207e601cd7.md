```
version control: it's a foundational piece of any project's infrastructure. Yet half of all project teams in the U.S. don't use any version control at all. Many others don't use it well, and end up experiencing time-consuming problems.
</p>},
:image_url => '/images/svn.jpg',
:price => 28.50)
# ...

Product.create(:title => 'Pragmatic Unit Testing (C#)',
:description =>
%{<p>
Pragmatic programmers use feedback to drive their development and personal processes. The most valuable feedback you can get while coding comes from unit testing.
</p>
<p>
Without good tests in place, coding can become a frustrating game of "whack-a-mole." That's the carnival game where the player strikes at a mechanical mole; it retreats and another mole pops up on the opposite side of the field. The moles pop up and down so fast that you end up flailing your mallet helplessly as the moles continue to pop up where you least expect them.
</p>};
:image_url => '/images/utc.jpg',
:price => 27.75)

end

def self.down
  Product.delete_all
end
end
Download depot1/db/migrate/20080601000004_create_sessions.rb
class CreateSessions < ActiveRecord::Migration
  def self.up
    create_table :sessions do |t|
      t.string :session_id, :null => false
      t.text :data
      t.timestamps
    end

    add_index :sessions, :session_id
    add_index :sessions, :updated_at
  end

  def self.down
    drop_table :sessions
  end
end
```