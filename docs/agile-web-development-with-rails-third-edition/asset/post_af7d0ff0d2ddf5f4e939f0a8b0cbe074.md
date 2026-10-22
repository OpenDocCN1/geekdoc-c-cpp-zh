
puts now.advance(:days => 30)      #=> Sat Jun 17 23:36:10 CDT 2006
puts Time.days_in_month(2)         #=> 28
puts Time.days_in_month(2, 2000)   #=> 29
puts now.xmlschema                 #=> "2006-05-18T23:36:10-06:00"

Rails 2.1 introduces time zone support. You can set the default time zone in config/environment.rb:

config.time_zone = 'UTC'

Within an action, you can override the time zone and convert any time to the indicated time zone:

Time.zone = 'Eastern Time (US & Canada)'
puts Time.now.in_time_zone

Active Support also includes a TimeZone class. TimeZone objects encapsulate the names and offset of a time zone. The class contains a list of the world's time zones. See the Active Support RDoc for details.

Rails 2.2 introduces three methods that query a given time: past?, today?, and future? query whether a given time is before now, is on today's date, or is in the future, respectively.

Date objects also pick up a few useful methods:

date = Date.today
puts date.tomorrow                 #=> "Fri, 19 May 2006"
puts date.yesterday                #=> "Wed, 17 May 2006"
puts date.current                  #=> "Thu, 18 May 2006"

current returns Time.zone.today when config.time_zone is set; otherwise, it just returns Date.today:

puts date.to_s                     #=> "2006-05-18"
puts date.xmlschema                #=> "2006-05-18T00:00:00-06:00"
puts date.to_time                  #=> Thu May 18 00:00:00 CDT 2006
puts date.to_s(:short)             #=> "18 May"
puts date.to_s(:long)              #=> "May 18, 2006"
puts date.to_s(:db)                #=> "2006-05-18"

The last of these converts a date into a string that's acceptable to the default database currently being used by your application. You may have noticed that the Time class has a similar extension for formatting datetime fields in a database-specific format.

You can add your own extensions to date and time formatting. For example, your application may need to display ordinal dates (the number of days into a year). The Ruby Date and Time libraries both support the strftime method for formatting dates, so you could use something like this:

>> d = Date.today
=> #<Date: 4907769/2,0,2299161>
>> d.to_s
=> "2006-05-29"
>> d.strftime("%y-%j")
=> "06-149"

Instead, though, you might want to encapsulate this formatting by extending the to_s method of dates. In your environment.rb file, add a line like the following:

ActiveSupport::CoreExtensions::Date::Conversions::DATE_FORMATS.merge!(
  :ordinal => "%Y-%j"
)

Now you can say this:

any_date.to_s(:ordinal)    #=> "2006-149"

You can extend the Time class string formatting as well:

ActiveSupport::CoreExtensions::Time::Conversions::DATE_FORMATS.merge!(
  :chatty => "It's %I:%M%p on %A, %B %d, %Y"
)
Time.now.to_s(:chatty)    #=> "It's 12:49PM on Monday, May 29, 2006"

There are also two useful time-related methods added to the String class. The methods to_time and to_date return Time and Date objects, respectively:

puts "2006-12-25 12:34:56".to_time    #=> Mon Dec 25 12:34:56 UTC 2006
puts "2006-12-25 12:34:56".to_date    #=> 2006-12-25

### 16.7 An Extension to Ruby Symbols

(As of Ruby 1.8.7, this feature is now a part of the language, but users of Rails making use of prior versions of the language can also make use of this feature).

We often use iterators where all the block does is invoke a method on its argument. We did this in our earlier group_by and index_by examples:

groups = posts.group_by { |post| post.author_id }

Rails has a shorthand notation for this. We could have written this code as this:

groups = posts.group_by(&:author_id)

Similarly, the following code:

us_states = State.find(:all)
state_lookup = us_states.index_by { |state| state.short_name }

could also be written like this:

us_states = State.find(:all)
state_lookup = us_states.index_by(&:short_name)

### 16.8 with_options

Many Rails methods take a hash of options as their last parameter. You'll sometimes find yourself calling several of these methods in a row, where each

We'll keep the controller simple by using a single action:

class PeopleController < ApplicationController

  def index
    @person = Person.new(params[:person])
    @person.save! if request.post?
    @people = Person.find(:all)
  end
end

The database is Unicode-aware. Now we just need to make sure that the browser side is too.

As of Rails 1.2, the default content-type header is as follows:

Content-Type: text/html; charset=UTF-8

However, just to be sure, we'll also add a <meta> tag to the page header to enforce this. This also means that if a user saves a page to a local file, it will display correctly later. This is our layout file:

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8"/>
<title>My Name List</title>
</head>
<body>
<%= yield :layout %>
</body>
</html>

In our index view, we'll show the full list of names in the database and provide a simple form to let folks enter new ones. In the list, we'll display the name and its size in bytes and characters, and, just to show off, we'll reverse it.

<table border="1">
<tr>
<th>Name</th><th>bytes</th><th>chars</th><th>reversed</th>
</tr>
<% for person in @people %>
<tr>
<td><%=h person.name %></td>
<td><%= person.name.length %></td>
<td><%= person.name.chars.length %></td>
<td><%=h person.name.chars.reverse %></td>
</tr>
<% end %>
</table>

<% form_for :person do |form| %>
  New name: <%= form.text_field :name %>
  <%= submit_tag "Add" %>
<% end %>

When we point our browser at our people controller, we'll see an empty table. Let's start by entering "Dave" in the name field:

![](img/a160fc3a330a0b3b2a764d41d614e688_288_0.png)

When we hit the Add button, we see that the string "Dave" contains both 4 bytes and 4 characters—normal ASCII characters take 1 byte in UTF-8:

![](img/a160fc3a330a0b3b2a764d41d614e688_288_1.png)

When we hit Add after typing Günter, we see something different:

![](img/a160fc3a330a0b3b2a764d41d614e688_288_2.png)

Because the ü character takes 2 bytes to represent in UTF-8, we see that the string has a byte length of 7 and a character length of 6. Notice that the reversed form displays correctly.

Finally, we'll add some Japanese text:

![](img/a160fc3a330a0b3b2a764d41d614e688_288_3.png)

Now the disparity between the byte and character lengths is even greater. However, the string still reverses correctly, on a character-by-character basis.

## Chapter 17: Migrations

Rails encourages an agile, iterative style of development. We don’t expect to get everything right the first time. Instead, we write tests and interact with our customers to refine our understanding as we go.

For that to work, we need a supporting set of practices. We write tests to help us design our interfaces and to act as a safety net when we change things, and we use version control to store our application’s source files, allowing us to undo mistakes and to monitor what changes day to day.

But there’s another area of the application that changes, an area that we can’t directly manage using version control. The database schema in a Rails application constantly evolves as we progress through the development: we add a table here, rename a column there, and so on. The database changes in step with the application’s code.

Historically, that has been a problem. Developers (or database administrators) make schema changes as needed. However, if the application code is rolled back to a previous version, it was hard to undo the database schema changes to bring the database back in line with that prior application version—the database itself has no versioning information.

Over the years, developers have come up with ways of dealing with this issue. One scheme is to keep the Data Definition Language (DDL) statements that define the schema in source form under version control. Whenever you change the schema, you edit this file to reflect the changes. You then drop your development database and re-create the schema from scratch by applying your DDL. If you need to roll back a week, the application code and the DDL that you check out from the version control system are in step. When you re-create the schema from the DDL, your database will have gone back in time.

Except…because you drop the database every time you apply the DDL, you lose any data in your development database. Wouldn’t it be more convenient
