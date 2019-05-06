# Thermostat API

```shell
bundle init
bundle add sinatra
bunlde add thermostat_FIRSTNAME_LASTNAME
bundle install
```

import insomnia settings file (`thermsotat_2019-05-06.json`) -> testing REST requests

create `app.rb` file

```ruby
require 'sinatra/base'
require 'whatever-you-need'

class MyApp < Sinatra::Base

  # add a setting 'foo', with the value of 'bar' to the Sinatra app
  set :foo = "bar"

  # before handling every route, set the 'content_type' to json (http header)
  before do
    content_type :json
  end

  get '/thermostat' do
    if settings.foo == "bar"
      status 400
      return '{"error": "foo is equal to bar"}'
    end
    '{"Hello": "world"}'
  end

  put '/thermostat' do
    request.body.rewind       # body is an IO object, and should be rewinded befor reading
    puts request.body.read
  end

  post '/thermostat' do
    request.body.rewind       # body is an IO object, and should be rewinded befor reading
    settings.bar = request.body.read
  end
end

MyApp.run!
```
