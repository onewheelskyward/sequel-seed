# Sequel::Seed [![Gem Version](https://badge.fury.io/rb/sequel-seed.svg)](http://badge.fury.io/rb/sequel-seed) [![Build Status](https://travis-ci.org/earaujoassis/sequel-seed.svg?branch=master)](https://travis-ci.org/earaujoassis/sequel-seed) [![Coverage Status](https://coveralls.io/repos/earaujoassis/sequel-seed/badge.svg?branch=master&service=github)](https://coveralls.io/github/earaujoassis/sequel-seed?branch=master)

> A Sequel extension to make seeds/fixtures manageable like migrations

## Usage

Create a seed file (eg. `/path/to/seeds/20150928000000_initial_seed.rb`)

```rb
Sequel.seed(:development, :test) do # Applies only to "development" and "test" environments
  def run
    [
      ['USD', 'United States dollar'],
      ['BRL', 'Brazilian real']
    ].each do |abbr, name|
      Currency.create abbr: abbr, name: name
    end
  end
end
```

Set the environment

```rb
Sequel::Seed.setup :development
```

Load the extension

```rb
require 'sequel'
require 'sequel/extensions/seed'

Sequel.extension :seed
```

Apply the seeds/fixtures

```rb
DB = Sequel.connect(...)
Sequel::Seeder.apply(DB, "/path/to/seeds")
```

For more information, please check the [project website](//earaujoassis.github.io/sequel-seed/).

## Limitations

- JSON and YAML files don't work with associations
- Only timestamped seed/fixture files

## What's next?

Work with Model's associations inside JSON &amp; YAML files

## Support

If you need any help (or have found any bug &#x1f41e;), please post it on
[/issues](//github.com/earaujoassis/sequel-seed/issues). Thank you!

## License

[MIT License](http://earaujoassis.mit-license.org/) &copy; Ewerton Assis
