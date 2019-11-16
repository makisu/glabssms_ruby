# Globe Labs SMS Ruby Library

Send SMS using [Globe Labs](http://www.globelabs.com.ph/developer/api) in Ruby.

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'glabssms'
```

Or install it yourself as:

```ruby
gem install glabssms
```

## Usage

In an initializer:

```ruby
Glabssms.configure do |c|
  c.app_id = 'GLABS_APP_ID'
  c.app_secret = 'GLABS_APP_SECRET'
  c.cross_telco_short_code = 'GLABS_CROSS_TELCO_SHORT_CODE'
  c.short_code = 'GLABS_SHORT_CODE'
end
```

## Initializing a Client

This is the instance that you will be interacting with to send SMS.

```ruby
# This client grabs defaults from config
client = Glabssms::Client.new(Glabssms::Configuration.new)

# Only to override the defaults that were set in config
client = Glabssms::Client.new(
  app_id: "...",
  app_secret: "...",
  cross_telco_short_code: "...",
  short_code: "..."
)
```

## Fetching Access Token after Subscriber Opt-In

```ruby
result = client.get_token(
  code: code_from_opt_in
)

# result will be an instance of TokenResult
token_from_subscriber_opt_in = result.token
subscriber_number = result.number
```

## Sending SMS

```ruby
result = client.send_sms(
  number: subscriber_number, # Can be in the form +639171234567 or 09171234567
  message: 'max_160_character_string',
  token: token_from_subscriber_opt_in
)
```

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake spec` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/makisu/glabssms_ruby. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).

## Code of Conduct

Everyone interacting in the Glabssms project’s codebases, issue trackers, chat rooms and mailing lists is expected to follow the [code of conduct](https://github.com/makisu/glabssms_ruby/blob/master/CODE_OF_CONDUCT.md).
