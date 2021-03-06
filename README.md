# Integer Permutation

[![Bitdeli](https://d2weczhvl823v0.cloudfront.net/attilaolah/intperm.go/trend.png)](https://bitdeli.com/free "Bitdeli Badge")
[![Build Status](https://travis-ci.org/attilaolah/intperm.go.png?branch=master)](https://travis-ci.org/attilaolah/intperm.go)
[![GoDoc](https://godoc.org/github.com/attilaolah/intperm.go?status.png)](https://godoc.org/github.com/attilaolah/intperm.go)

This package implements a simple, configurable permutation on the set of 64-bit
integers.

The permutation is based on a bitmask that maps each bit of the input to a bit
of the output. The bitmask is expanded from a random seed using a [PRNG][1], as
described by *George Marsaglia* in his paper called [Xorshift RNGs][2]. The
permutations are thus believed to be unpredictable, provided provided that the
seed is kept secret.

[1]: //en.wikipedia.org/wiki/Pseudorandom_number_generator
[2]: http://www.jstatsoft.org/v08/i14/paper

## Usage

Create a new `Permutation` instance by passing in a seed:

```go
p := permutation.New(42)
a := p.MapTo(37) // 13750393542137160527
b := p.MapFrom(13750393542137160527) // 37
```

## Use cases

Use cases may vary, but an example that I find useful is generating
[hard][4]-to-guess, random-looking tokens based on IDs stored in a database.
The IDs can be used together with the seed to decode the original ID, but their
[cardinality][5] is the same as that of the IDs themselves. When used smartly,
this can save you from having to index those tokens in the database.

Another good example is randomising IDs of private objects that are available
via some sort of an API. Let's say the user accounts on your website are
accessible via the path `/user/:id`, where `:id` is the user's ID. Someone
could track the growth of your user base just by enumerating the URLs and
keeping track of the status codes (e.g. 403 vs. 404).

Using this simple permutation, user IDs can be kept unpredictable, rendering
these kinds of attacks practically useless.

[4]: //en.wikipedia.org/wiki/NP-hard
[5]: //en.wikipedia.org/wiki/Cardinality

## See also

This library is also implemented in [Python][7] and [Ruby][6].

[6]: //github.com/attilaolah/intperm.rb
[7]: //github.com/attilaolah/intperm.py
