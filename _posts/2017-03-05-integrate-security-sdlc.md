---
layout: post
title: Integrating Security Into Your SDLC Using RSpec After Hooks
description: ""
tags: [sdlc, rspec, security]
---

There are 2 concepts I'd like to share that can really help to eliminate the low-hanging fruit of
security vulnerabilities. Those are, static code analysis and dependency checking.

Static code analysis scans all of your code and looks for known vulnerable patterns. It won't
find complex flaws in business logic, but it'll raise red flags if a developer ever adds something
like <code>Widget.where("name = #{name}")</code> into the code. (For those who may not know, this opens a
SQL injection vulnerability.)

Dependency checking looks at what 3rd party libraries are being used and their versions, and checks
this data against a database of known vulnerabilities. For example, did you know the Administrate
gem below version 0.1.5 has a CSRF vulnerability? How about any other gems in your Gemfile?

There are 2 great tools that can help us out in Ruby: [Brakeman](http://brakemanscanner.org/)
and [Bundler-Audit](https://github.com/rubysec/bundler-audit).

Brakeman is an excellent open-source static code analysis tool with a number of options for tweaking
its reports. Bundler-Audit will scan the Gemfile.lock and compare against the Ruby advisory db.
These tools are great on their own, and each comes with an executable that can be run on the
command line. However, manually running them every time you write new code or change gems adds
extra work and is very easy to forget. Don't worry, there's a great, simple way to add them to our testing
cycle, so that every time we run our tests, our code is analyzed as well.

First, you'll need to add them to your Gemfile:
```ruby
group :development, :test do
  gem 'brakeman', '~> 3.5'
  gem 'bundler-audit'
end
```

Next, create an `after(:suite)` hook in your `spec_helper.rb`:
```ruby
config.after(:suite) do
    examples = RSpec.world.filtered_examples.values.flatten
    after_hooks = ["brakeman -w2 -z --no-summary", "bundle-audit --update"]
    if examples.none?(&:exception)
      after_hooks.each do |hook_command|
        system("echo ' ' && #{hook_command}")
        exitstatus = $?.exitstatus
        exit exitstatus if exitstatus.nonzero?
      end
    end
  end
```

That one is a little less obvious, so let me break it down a bit.

The first thing we do is grab all the examples that run. If any of our tests failed, we don't run
the hooks. If all the tests are green, then we'll run brakeman. If it reports any vulnerabilities,
it'll exit with a nonzero status, per the `-z` flag. If all is good, we'll move onto bundler-audit,
which will update the advisory database and scan the `Gemfile.lock`.

Again, if vulnerabilities are reported, it'll exit with a non-zero status code, which
will cause the build to go red in your continuous integration service.

So that's it, with very little code, and not much work, we've fully integrated static code analysis
and dependency checking into our development lifecycle in a way that can't be overlooked.
