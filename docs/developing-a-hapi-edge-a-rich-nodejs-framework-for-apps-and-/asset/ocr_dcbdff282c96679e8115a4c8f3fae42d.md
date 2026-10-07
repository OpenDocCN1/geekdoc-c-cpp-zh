# Models

pipe it to /dev/null... is it web scale?

-- Humorous video regarding MongoDB

Models provide the backbone for any useful web application. They are responsible for managing data: connecting to sources of data, reading data, creating data, and so on. Decisions regarding data - including database choices, schema design, and index design - all have a huge impact on how an application performs or behaves.

Data can come from anywhere: from the web, from a database, from a file, or a service. For our hapi-plugins application, we will be focusing on getting our data from the web via HTTP and from a database.

# Using HTTP

One popular way to obtain data for an application is to use third party web APIs. Your application may want to connect to Twitter, Facebook, or Google APIs. Most of these services offer RESTful APIs over HTTP or HTTPS. These types of APIs are extremely easy to work with and can be called from any programming language or operating system.

# Desired Usage

Prior to coding the hapi-plugins application, we analyzed the NPM API and determined that there were eight relevant APIs:

+   - Getting list of plugin names
- Getting list of plugins matching an input keyword search
- Getting list of plugins by name
- Getting list of plugins by depended on
- Getting plugin download count by day
- Getting plugin download count by week
- Getting plugin download count by month