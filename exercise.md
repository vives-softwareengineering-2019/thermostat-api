# Thermostat API

Build an HTTP API that functions as an thermostat. To achieve this, some REST routes should be provided:

* `GET /thermostat`: Get the status of the heating and cooling calculated by the thermostat.
* `PUT /thermostat`: Update/create a thermostat providing a JSON object, containing the wanted temperature and range.
* `POST /thermostat`: Update the temperature, triggering a recalculation fo the heating and cooling states.

All input and out should consist out of JSON objects.

Make use of HTTP status codes to signal if a request is handled correctly (status code 200), of if anything went wrong (status code 400 and variants).

A configuration file for the tool Insomnia is provided in the root of this project. [thermsotat_2019-05-06.json](thermsotat_2019-05-06.json)). The file will add some preconfigured HTTP request to Insomnia to help you develop this Thermostat API application.

## Sinatra

Sinatra is a DSL for quickly creating web applications in Ruby with minimal effort.

Webiste: [http://sinatrarb.com/](http://sinatrarb.com/).

```ruby
require 'sinatra'
get '/frank-says' do
  'Put this in your pipe & smoke it!'
end
```

Most of its usage is documented in the get started: [http://sinatrarb.com/intro.html](http://sinatrarb.com/intro.html)

## Package management with Bundler

To manage packages and dependencies, a package manager is needed. The most popular package manager for Ruby is Bundler. Bundlers provides some `bundle` commands to help you manage packages.

```shell
bundle init
bundle add sinatra
bunlde add thermostat_FIRSTNAME_LASTNAME
bundle install
```

## Thermostat API application

Create an `app.rb` file, and start building the Thermostat API application that will respond to the HTTP routes defined above.

## Sinatra Example application

This is just an example applications that demonstrates some useful concepts that could assist you with building the Thermostat API application.

```ruby
require 'sinatra/base'
require 'whatever-you-need'

class MyApp < Sinatra::Base

  # add a setting 'foo', with the value of 'bar' to the Sinatra app. See: http://sinatrarb.com/configuration.html
  set :foo = "bar"

  # before handling every route, set the 'content_type' to json (http header). See: http://sinatrarb.com/intro.html filters
  before do
    content_type :json
  end

  # GET route
  get '/demo' do
    if settings.foo == "bar"
      status 400
      return '{"error": "foo is equal to bar"}'
    end
    '{"Hello": "world"}'
  end

  # PUT route
  put '/demo' do
    request.body.rewind       # body is an IO object, and should be rewinded befor reading
    puts request.body.read
  end

  # POST route
  post '/demo' do
    request.body.rewind       # body is an IO object, and should be rewinded befor reading
    settings.bar = request.body.read
  end
end

MyApp.run!
```

## Docker

When the application is implemented and tested, create A `Dockerfile` containing a configuration to run the application in a docker container.
The container should expose port 80.

```ruby
set :port, 80
set :bind, '0.0.0.0'
```
