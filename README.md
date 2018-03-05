**Note: This is a fork maintained mainly for Storyful's use that will merge only
security updates to keep the project stable.**

# XmlHasher

[![Build Status](https://travis-ci.org/cloocher/xmlhasher.png)](https://travis-ci.org/cloocher/xmlhasher)
[![Gem Version](https://badge.fury.io/rb/xmlhasher.png)](http://badge.fury.io/rb/xmlhasher)

Fast XML to Ruby Hash converter

## Installation

XmlHasher is available through [Rubygems](http://rubygems.org/gems/xmlhasher) and can be installed via:

```
$ gem install xmlhasher
```

or add it to your Gemfile like this:

```
gem 'xmlhasher'
```

## Usage

```ruby
require 'xmlhasher'

# XmlHasher global configuration
#
# snakecase - convert all keys to snake case notation
# ignore_namespaces - remove XML namespaces
# string_keys - represent keys as Strings instead of Symbols
#
# here is default configuration
XmlHasher.configure do |config|
  config.snakecase = true
  config.ignore_namespaces = true
  config.string_keys = false
end

# alternatively, specify configuration options when instantiating a Parser
parser = XmlHasher::Parser.new(
  :snakecase => true,
  :ignore_namespaces => true
  :string_keys => false
)

# by default, XmlHasher will convert all keys to symbols.  If you want all keys to be Strings, set :string_keys option to 'true'

# parse XML file
XmlHasher.parse(File.new('/path/to/my/file.xml'))

# parse XML string
XmlHasher.parse("<tag1><tag2>content</tag2></tag1>")
# => {:tag1=>{:tag2=>"content"}}

```
## Benchmarks

How fast is it?  Try it for yourself - [benchmark.rb](https://github.com/cloocher/xmlhasher/blob/master/benchmark/benchmark.rb)

```
Converting small xml from text to Hash:

                            user     system      total        real
activesupport(rexml)     0.380000   0.000000   0.380000 (  0.385326)
activesupport(libxml)    0.060000   0.000000   0.060000 (  0.062008)
activesupport(nokogiri)  0.090000   0.000000   0.090000 (  0.089466)
xmlsimple                0.480000   0.010000   0.490000 (  0.490938)
nori                     0.120000   0.000000   0.120000 (  0.123612)
xmlhasher                0.010000   0.000000   0.010000 (  0.017366)

Converting large xml from file to Hash:

                            user     system      total        real
activesupport(rexml)    57.230000   0.240000  57.470000 ( 57.460510)
activesupport(libxml)   # Segmentation fault
activesupport(nokogiri) 12.650000   0.250000  12.900000 ( 12.908073)
xmlsimple               49.980000   0.160000  50.140000 ( 50.140775)
nori                    15.590000   0.110000  15.700000 ( 15.697411)
xmlhasher                4.290000   0.030000   4.320000 (  4.316379)
```
Note: benchmarks were generated on a Macbook Pro using Ruby 1.9.3p392

## Requirements

* Ruby 1.9.3 or higher

## Copyright
Copyright (c) 2013 Gene Drabkin.
See [LICENSE][] for details.

[license]: LICENSE.md
