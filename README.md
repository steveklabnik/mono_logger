# MonoLogger

Ruby's stdlib Logger wraps all IO in mutexes. Ruby 2.0 doesn't allow you to
request a lock in a trap handler because that could deadlock. This gem fixes
this issue by giving you a lock-free logger class.

If you've ever seen `log writing failed. can't be called from trap context`,
you're in the right place!

## Installation

Add this line to your application's Gemfile:

    gem 'mono_logger'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install mono_logger

## Usage

It's simple, just use `MonoLogger` anywhere you'd use `Logger`:

```ruby
require 'logger'


logger = Logger.new(STDOUT)
logger.level = Logger::WARN

logger.debug("Created logger")
logger.info("Program started")
logger.warn("Nothing to do!")
```

Turns into

```ruby
require 'mono_logger'


logger = MonoLogger.new(STDOUT)
logger.level = MonoLogger::WARN

logger.debug("Created logger")
logger.info("Program started")
logger.warn("Nothing to do!")
```

That's it! No more errors!

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request

## License

MonoLogger was originally created for Chef:
https://github.com/opscode/chef/commit/634ad58ab14d6cfa05f56991bbc758cc3b22d410

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

A copy of the License is included in the LICENSE.txt file included with this
source code.
