# Jortt REST API client

[![Inline docs](
http://inch-ci.org/github/jorttbv/jortt-ruby.svg?branch=master&style=flat
)](http://inch-ci.org/github/jorttbv/jortt-ruby)
[![Code Climate](
http://img.shields.io/codeclimate/github/jorttbv/jortt-ruby.svg?style=flat
)](https://codeclimate.com/github/jorttbv/jortt-ruby)
[![Code Coverage](
https://codecov.io/github/jorttbv/jortt-ruby/coverage.svg?branch=master
)](https://codecov.io/github/jorttbv/jortt-ruby?branch=master)
[![Build Status](
http://img.shields.io/travis/jorttbv/jortt-ruby.svg?style=flat
)](https://travis-ci.org/jorttbv/jortt-ruby)

A Ruby interface to the [Jortt](https://www.jortt.nl/) REST API.

## Usage

To create a jortt client:
```ruby
jortt = Jortt.client(
  app_name: "application-name-as-chosen-on-jortt.nl",
  api_key: "api-key-as-provided-by-jortt.nl"
)
```

### Customers

Accessing customers (`jortt.customers.search('Jortt')`) returns:
```ruby
[{
  company_name: 'Jortt',
  address: {
    street: "Transistorstraat 71C",
    postal_code: "1322 CK",
    city: "Almere",
    country_code: "NL"
  }
},
  company_name: 'ttroj',
  address: {
    street: "Jorttweg",
    ...
  }
}]
```

Adding customers:
```ruby
jortt.customers.create(
  company_name: "Jortt B.V.",
  attn: "Vibiemme", # Optional
  extra_information: "The best cofee maker!", # Optional
  address: {
    street: "Transistorstraat 71C",
    postal_code: "1322 CK",
    city: "Almere",
    country_code: "NL"
  }
)
```

### Invoices

Adding invoices:
```ruby
jortt.invoices.create(
  customer_id: "123456789", # Optional
  delivery_period: "31-12-1234", # Optional
  reference: "my-reference", # Optional
  line_items: [
    {vat: 21, amount: 1359.50, quantity: 1, description: "Scrum Training"}
  ]
)
```

## Documentation

Check https://app.jortt.nl/api-documentatie for more info.

## Development

### Running tests

`bundle install` and then `rake spec` or `rspec spec`.

### Building the gem

`rake build` and then `rake install` to test it locally (`irb` followed
by `require 'jortt/client'` and do your stuff).

### Releasing the gem

Make a fix, commit and push. Make sure the build is green. Then bump the
version (edit `lib/jortt/client/version.rb`). Now `rake release` and follow
the instructions (you need a rubygems.org account and permissions ;-)).
