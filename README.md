# RedisGCRA
[![Build Status](https://travis-ci.org/rwz/redis-gcra.svg?branch=master)](https://travis-ci.org/rwz/redis-gcra)

This gem is an implementation of GCRA for rate limiting based on Redis. The
code requires Redis version 3.2+ or newer since it relies on
[`replicate_comands`][redis-replicate-commands] feature.

[redis-replicate-commands]: https://redis.io/commands/eval#replicating-commands-instead-of-scripts
## Installation

```ruby
gem "redis-gcra"
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install redis-gcra

## Usage

```ruby
redis = Redis.new

result = RedisGCRA.limit(
  redis: redis,
  key: "rate-limit-key",
  burst: 1000,
  rate: 100,
  period: 60,
  cost: 2
)

result.limited?    # => false - request should not be limited
result.remaning    # => 999   - remaningn number of request until limited
result.retry_after # => nil   - can retry without delay
result.reset_after # => ~0.6  - in 0.6s limit will completely reset
```

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

