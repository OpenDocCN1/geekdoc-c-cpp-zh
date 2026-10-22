
manage. What it does is put the version of the software that you are dependent on into the repository:

```
$ rake rails:freeze:gems
$ rake gems:unpack
$ git add vendor
$ git commit -m "freeze gems"
```

From here, it is a simple matter to push all your code out to the server:

```
$ git remote add origin ssh://user@host/~/git/depot.git
$ git push origin master
```

## Deploying the Application

The prep work is now done. Our code is now on the SCM server where it can be accessed by the app server.⁵ Now we can install Capistrano via gem install capistrano.

To add the necessary files to the project for Capistrano to do its magic, execute the following command:

```
$ capify .
[add] writing './Capfile'
[add] writing './config/deploy.rb'
[done] capified!
```

From the output, we can see that Capistrano set up two files. The first, Capfile, is Capistrano's analog to a Rakefile. We won't need to touch this file further. The second, config/deploy.rb, contains the recipes needed to deploy our application. Capistrano will provide us with a minimal version of this file, but the following is a somewhat more complete version that you can download and use as a starting point:

Download config/deploy.rb

```
# be sure to change these
set :user, 'rubys'
set :domain, 'depot.pragprog.com'
set :application, 'depot'

# file paths
set :repository, "#{user}@#{domain}:git/#{application}.git"
set :deploy_to, "/home/#{user}/#{domain}"

# distribute your applications across servers (the instructions below put them
# all on the same server, defined above as 'domain', adjust as necessary)
role :app, domain
role :web, domain
role :db, domain, :primary => true
```

> 5. It matters not whether these two servers are the same; what is important here is the roles that are being performed.

```
# you might need to set this if you aren't seeing password prompts
# default_run_options[:pty] = true

# As Capistrano executes in a non-interactive mode and therefore doesn't cause
# any of your shell profile scripts to be run, the following might be needed
# if (for example) you have locally installed gems or applications. Note:
# this needs to contain the full values for the variables set, not simply
# the deltas.
# default_environment['PATH']='<your paths>:/usr/local/bin:/usr/bin:/bin'
# default_environment['GEM_PATH']='<your paths>:/usr/lib/ruby/gems/1.8'

# miscellaneous options
set :deploy_via, :remote_cache
set :scm, 'git'
set :branch, 'master'
set :scm_verbose, true
set :use_sudo, false
```

```
# task which causes Passenger to initiate a restart
namespace :deploy do
  task :restart do
    run "touch #{current_path}/tmp/restart.txt"
  end
end
```

```
# optional task to reconfigure databases
after "deploy:update_code", :configure_database
desc "copy database.yml into the current release path"
task :configure_database, :roles => :app do
  db_config = "#{deploy_to}/config/database.yml"
  run "cp #{db_config} #{release_path}/config/database.yml"
end
```

We will need to edit several properties to match our application. We certainly will need to change the :user, :domain, and :application. The :repository matches where we put our Git file earlier. The :deploy_to may need to be tweaked to match where we told Apache it could find the config/public directory for the application.

The default_run_options and default_environment are to be used only if you have specific problems. The “miscellaneous options” provided are based on Git.

Two tasks are defined. One tells Capistrano how to restart Passenger. The other updates the file database.yml from the copy that we previously placed on the sever. Feel free to adjust these tasks as you see fit.

The first time we deploy our application, we have to perform an additional step to set up the basic directory structure to deploy into on the server:

```
$ cap deploy:setup
```

When we execute this command, Capistrano will prompt us for our server's password. If it fails to do so and fails to log in, we might need to uncomment out the default_run_options line in our deploy.rb file and try again. Once it can

## Looking at Log Files

To get a quick look at what’s happening in our application, we can use the tail command to examine log files as requests are made against our application. The most interesting data will usually be in the log files from the application itself. Even if Apache is running multiple applications, the logged output for each application is placed in the production.log file for that application.

Assuming that our application is deployed into the location we showed earlier, here’s how we look at our running log file:

```
# On your server
$ cd /home/rubys/work/depot/
$ tail -f log/production.log
```

Sometimes, we need lower-level information—what’s going on with the data in our application? When this is the case, it’s time to break out the most useful live server debugging tool.

## Using Console to Look at a Live Application

We’ve already created a large amount of functionality in our application’s model classes. Of course, we created these to be used by our application’s controllers. But we can also interact with them directly. The gateway to this world is the script/console script. We can launch it on our server with this:

```
# On your server
$ cd /home/rubys/work/depot/
$ ruby ./script/console production
Loading production environment.
irb(main):001:0> p = Product.find_by_title("Pragmatic Version Control")
=> #<Product:0x24797b4 @attributes={. . .}>
irb(main):002:0> p.price = 32.95
=> 32.95
irb(main):003:0> p.save
=> true
```

Once we have a console session open, we can poke and prod all the various methods on our models. We can create, inspect, and delete records. In a way, it’s like having a root console to your application.

## 28.6 Production Application Chores

Once you put an application into production, we need to take care of a few chores to keep your application running smoothly. These chores aren’t automatically taken care of for us, but, luckily, we can automate them.

## Dealing with Log Files

As an application runs, it will constantly add data to its log file. Eventually, the log files can grow extremely large. To overcome this, most logging solutions

can roll over log files to create a progressive set of log files of increasing age. This will break up our log files into manageable chunks that can be archived off or even deleted after a certain amount of time has passed.

The Logger class supports rollover. We simply need to decide how many (or how often) log files we want and the size of each. To enable this, simply add a line like one of the following to the file config/environments/production.rb:

```
```ruby
config.logger = Logger.new(config.log_path, 10, 10.megabytes)
config.logger = Logger.new(config.log_path, 'daily')
```
```

Alternately, we can direct our logs to the system logs for our machine:

```
```ruby
config.logger = SyslogLogger.new
```
```

Find more options at [http://wiki.rubyonrails.com/rails/pages/DeploymentTips](http://wiki.rubyonrails.com/rails/pages/DeploymentTips).

## Clearing Out Sessions

If you are not using cookie-based session management, be aware that the session handler in Rails doesn’t do automated housekeeping. This means that once the data for a session is created, it isn’t automatically cleared out after the session expires. This can quickly spell trouble. The default file-based session handler will run into trouble long before the database-based session handler will, but both handlers will create an endless amount of data.

Since Rails doesn’t clean up after itself, we’ll need to do it ourselves. The easiest way is to run a script periodically. If we keep sessions in files, the script needs to look at when each session file was last touched and then delete the older ones. For example, we could put the following command into a script that will delete files that haven’t been touched in the last twelve hours:

```
```bash
# On your server
$ find /tmp/ -name 'ruby_sess:*' -ctime +12h -delete
```
```

If our application keeps session data in the database, our script can look at the updated_at column and delete rows accordingly. We can use script/runner to execute this command:

```
```bash
> RAILS_ENV=production ./script/runner  \
    CGI::Session::ActiveRecordStore::Session.delete_all( \
      ["updated_at < ?", 12.hours.ago])
```
```

## Keeping on Top of Application Errors

Controller actions that fail are handled differently in development vs. production. In development, we get tons of debugging information. In production, the default behavior is to render a static HTML file with the name of the error code thrown. Custom rescue behavior can be achieved by overriding the rescue_action_in_public and rescue_action_locally methods. We can override what is
