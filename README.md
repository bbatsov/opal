# Opal

[![Build Status](http://img.shields.io/travis/opal/opal/master.svg?style=flat)](http://travis-ci.org/opal/opal)
[![Gem Version](http://img.shields.io/gem/v/opal.svg?style=flat)](http://badge.fury.io/rb/opal)
[![Code Climate](http://img.shields.io/codeclimate/github/opal/opal.svg?style=flat)](https://codeclimate.com/github/opal/opal)

Opal is a Ruby to JavaScript source-to-source compiler. It also has an
implementation of the Ruby corelib.

Opal is [hosted on GitHub](http://github.com/opal/opal). Chat is available on *Gitter* at [opal/opal](https://gitter.im/opal/opal) and the Freenode IRC channel at [#opal](http://webchat.freenode.net/?channels=opal).
Ask questions on [stackoverflow (tag #opalrb)](http://stackoverflow.com/questions/ask?tags=opalrb). Get the [Opalist newsletter](http://opalist.co) for updates and community news.

[![Inline docs](http://inch-ci.org/github/opal/opal.svg?branch=master&style=flat)](http://opalrb.org/docs/api)
[![Gitter chat](http://img.shields.io/badge/gitter-opal%2Fopal-009966.svg?style=flat)](https://gitter.im/opal/opal)
[![Stack Overflow](http://img.shields.io/badge/stackoverflow-%23opalrb-orange.svg?style=flat)](http://stackoverflow.com/questions/ask?tags=opalrb)

## Usage

See the website, [http://opalrb.org](http://opalrb.org).

### Compiling Ruby code

`Opal.compile` is a simple interface to just compile a string of Ruby into a
string of JavaScript code.

```ruby
Opal.compile("puts 'wow'")  # => "(function() { ... self.$puts("wow"); ... })()"
```

Running this by itself is not enough, you need the opal runtime/corelib.

### Building the corelib

`Opal::Builder` can be used to build the runtime/corelib into a string.

```ruby
Opal::Builder.build('opal') #=> "(function() { ... })()"
```

### Running compiled code

You can write the above two strings to files and run as:

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="opal.js"></script>
    <script src="app.js"></script>
  </head>
</html>
```

Just open this page in a browser and check the JavaScript console.

## Running tests

First, install dependencies:

    $ bundle install
    $ npm install -g jshint

RubySpec related repos must be cloned as git submodules:

    $ git submodule update --init

The test suite can be run using (requires [phantomjs][]):

    $ bundle exec rake

This will command will run all RSpec and MSpec examples in sequence.

#### Automated runs

A `Guardfile` with decent mappings between specs and lib/corelib/stdlib files is in place.
Run `bundle exec guard -i` to start `guard`.


### MSpec

[MSpec][] tests can be run with:

    $ rake mspec

Alternatively, you can just load up a rack instance using `rackup`, and
visit `http://localhost:9292/` in any web browser.


### Rspec

[RSpec][] tests can be run with:

    $ rake rspec


## Code Overview

What code is supposed to run where?

* `lib/` code runs inside your Ruby env. It compiles Ruby to JavaScript.
* `opal/` is the runtime/corelib for our implementation (runs in browser)
* `stdlib/` is our implementation of Ruby's stdlib. It is optional (for browser).

### lib

The `lib` directory holds the opal parser/compiler used to compile Ruby
into JavaScript. It is also built ready for the browser into `opal-parser.js`
to allow compilation in any JavaScript environment.

### corelib

This directory holds the opal runtime and corelib implemented in Ruby and
JavaScript.

### stdlib

Holds the stdlib that opal currently supports. This includes `Observable`,
`StringScanner`, `Date`, etc.

## Browser support

* Internet Explorer 6+
* Firefox (Current - 1) or Current
* Chrome (Current - 1) or Current
* Safari 5.1+
* Opera 12.1x or (Current - 1) or Current

Any problems encountered using the browsers listed above should be reported as bugs.

(Current - 1) or Current denotes that we support the current stable version of
the browser and the version that preceded it. For example, if the current
version of a browser is 24.x, we support the 24.x and 23.x versions.

12.1x or (Current - 1) or Current denotes that we support Opera 12.1x as well
as the last 2 versions of Opera. For example, if the current Opera version is 20.x,
then we support Opera 12.1x, 19.x and 20.x but not Opera 15.x through 18.x.

Cross-browser testing is sponsored by [BrowserStack](http://browserstack.com).

## License

(The MIT License)

Copyright (C) 2013-2015 by Adam Beynon

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.


[phantomjs]: http://phantomjs.org
[MSpec]: https://github.com/rubyspec/mspec#readme
[RSpec]: https://github.com/rspec/rspec#readme
