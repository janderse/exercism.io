# exercism.io
[![Stories in Ready](https://badge.waffle.io/exercism/exercism.io.svg?label=ready)](https://waffle.io/exercism/exercism.io)
[![Build Status](https://travis-ci.org/exercism/exercism.io.png?branch=master)](https://travis-ci.org/exercism/exercism.io)
[![Code Climate](https://codeclimate.com/github/exercism/exercism.io.png)](https://codeclimate.com/github/exercism/exercism.io)
[![Gemnasium](https://gemnasium.com/exercism/exercism.io.png)](https://gemnasium.com/exercism/exercism.io)
[![Coverage Status](https://coveralls.io/repos/exercism/exercism.io/badge.png?branch=master)](https://coveralls.io/r/exercism/exercism.io?branch=master)

Application to support working through sequential programming problems, with
crowd-sourced code reviews.

## WARNING

This is an experiment, and the code reflects that. Many features have been thrown
in, only to be deprecated shortly thereafter, and there's scar tissue
throughout the system.

Features may be here today, gone tomorrow.

Things do seem to have settled a bit in the past couple of months, so there's
a chance that we'll reach some sort of 1.0 in early 2014.

The messaging right now is a disaster. The site is confusing, the process is
opaque, and it's hard to figure out where you need to look to figure stuff
out.

### What we think we know

This is a process with two parts:

* practice (writing code, iterating)
* nitpicking (looking at code, providing insights and asking questions)

It's not about getting code perfect or right, but using the pieces of code to
talk about the little details of what makes code simple, readable, and/or
expressive.

## The Data

The warmup exercises are collected from all over the web.

The common data for assignments are in

```bash
assignments/shared
```

This includes some metadata that gets sewn into a README.

Not all assignments will be appropriate for all languages.

The actual assignment consists of a test suite, where all test are pending
except the first one.

The languages paths are configured in `lib/exercism/curriculum/LANGUAGE.rb`.

The list of assignments is just a really big array of assignment slugs in the order that they will be assigned.

Different languages/trails do not need to have the same assignments or the same order.

## Setup

1. Install postgresql with: `brew install postgresql` or `apt-get install postgresql-9.2`
2. Copy `.ruby-version.example` to `.ruby-version` if you use a Ruby version manager such as RVM, rbenv or chruby
3. Install gems with: `bundle`
4. Install `mailcatcher` with `gem install mailcatcher`
5. Get a client id/secret from GitHub at https://github.com/settings/applications/new.
  * Name: whatever
  * URL: http://localhost:4567
  * Callback url: http://localhost:4567/github/callback
6. Presuming you have Postgres installed (if not: `brew install postgres`):
  * create db user with: `createuser -s exercism`.
  * create database with: `createdb -O exercism exercism_development`.
7. Run the database migrations with `rake db:migrate`.
8. Run the database seed with `rake db:seed`. If you want LOTS of data: `rake db:seed[1000]` or some other big number.
9. Copy `config/env` to `.env`
10. Edit `.env` to fill in the correct values, including the GitHub client id/secret procured earlier.
11. Start the server with `foreman start`
12. Login at http://localhost:4567.
13. You can view the emails sent in [MailCatcher](http://mailcatcher.me/) in your browser at [localhost:1080](http://localhost:1080).
14. Work through 'Frontend development setup' below and run lineman for correct styling at http://localhost:4567

## Frontend development setup
1. Install node and npm
  * osx: brew install node
  * others see: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
2. Install lineman via `sudo npm install -g lineman`
3. `cd frontend` and start lineman with `lineman run`
  * note lineman watches for file changes and compiles them automatically, it is not required to be running for the server to run

## Sending Emails

If you want to send emails, you will need to fill out the relevant environment variables in `.env` and uncomment the lines so that the variables get exported.

## Console

There's a script in `bin/console` that will load pry with the exercism environment loaded.

## Testing

1. Prepare the test environment with `RACK_ENV=test rake db:migrate`.
2. Make sure that `mailcatcher` is running.
3. Run the test suite with `rake` or `rake test`.

To run a single test suite, you can do so with:

```bash
ruby path/to/the_test.rb
```

If it complains about dependencies, then either we forgot to require the correct dependencies (a distinct possibility), or we are dependening on a particular tag of a gem installed directly from github (this happens on occasion).

If there's a git dependency, you can do this:

```bash
bundle exec ruby path/to/the_test.rb
```

For the require, you'll need to figure out what the missing dependency is. Feel free to open an issue on github. It's likely that someone familiar with the codebase will be able to identify the problem immediately.

### Code coverage

To enable code coverage run:

```bash
COVERAGE=1 rake test
```

Browse the results located in `coverage/index.html`

## Deployment

Let Heroku know that Lineman will be building our assets. From the command line:
```
heroku config:set BUILDPACK_URL=https://github.com/testdouble/heroku-buildpack-lineman-ruby.git
```

## Contributing

Thank you for wanting to contribute! :heart::sparkling_heart::heart:

Fork and clone. Hack hack hack.
Submit a pull request and tell us why your idea is awesome.

For more details, please read the [contributing guide](https://github.com/exercism/exercism.io/blob/master/CONTRIBUTING.md).

To join the mailing list, send an email to exercism@librelist.com to be automatically subscribed or check out the [Archives](http://librelist.com/browser/exercism/).

## License

GNU Affero General Public License

Copyright (C) 2013 Katrina Owen, _@kytrinyx.com

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

