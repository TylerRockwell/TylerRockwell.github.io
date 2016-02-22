---
layout: post
title: Writing a Custom Namespaced Generator for your Rails Gem
description: "Custom generators can make things much easier for your users"
tags: [gem development, generators, rails, ruby]
---

So I had to write one of these recently, and quickly learned that there are far
fewer resources available than for a typical Rails project. Much of the information
that is up is scattered, outdated, or inaccurate. I've decided to write up a guide
for building and testing a custom generator so that users can install your gem
via `rails g my_gem:install`, rather than manually configuring everything.

There are quite a few resources available on starting a new gem,
[(here's one!)](https://quickleft.com/blog/engineering-lunch-series-step-by-step-guide-to-building-your-first-ruby-gem/)
so I won't bother explaining all of that. This post will start under the assumption that you have the
basics of a gem put together already.

### Step 1 - Create the Generator File

Generator files follow the convention of `task_name_generator.rb`. In our case
the file will be called `install_generator.rb`. This file should be in
`lib/generators/my_gem`. Note that the last folder is the
namespace. It often has the same name as the gem, but it doesn't have to. This name
will be the namespace of the task, so if you want a task that's called `taco_tuesday:install`,
then it should be placed in `lib/generators/taco_tuesday`.

Inside the file, the code should look like this.

``` ruby
require 'rails/generators'
module TacoTuesday
  module Generators
    class InstallGenerator < Rails::Generators::Base
      def code_that_runs
        puts "Hi"
      end
    end
  end
end
```

So, a few things here. First, this file needs to require `'rails/generators'`.
This will give us access to `Thor` actions, which will be important later.
Next, there are 2 modules. The first should match the namespace
and the second is always `Generators`. The class should always follow the convention of
`TaskGenerator`, so in our case, it's `InstallGenerator`. This class needs to inherit
from `Rails::Generators::Base`, and if the generator takes a parameter, then the class
needs to inherit from `Rails::Generators::NamedBase` instead.

All of the naming is important here. If a folder or module name is changed, the task
will show up when you run `rails g --help`, but when you try to run the generator,
it will say the task was not found. Note that `rails g --help` can only be run
in a Rails app that uses your gem. It cannot be run inside the gem's development folder.

### Step 2 - Make the Generator Do Something

From the code above, we'll be looking at the method `code_that_runs` This method
can be named whatever you like. The names do not follow conventions here.

Generators operate a bit differently than other classes. That is, when you call
a generator, it runs **all** of the public methods defined in the class. Also,
as I mentioned above, `Thor` actions are available. What does `Thor` do?
It provides a ton of useful methods and actions for you to use inside your generator.
There is a lot of good information in the [Thor Docs](http://www.rubydoc.info/github/wycats/thor/Thor/Actions).
A great example is if you need to append text inside a certain block in a file.
Let's say you need to place text inside the `RSpec.configure` block in the `spec_helper`.
With Thor, you can use the `insert_into_file` method, which takes a destination file,
text, and an optional regex with a `before` or `after` key. So it might look something
like this:

``` ruby
insert_into_file(destination, "\nTacoTuesday.initialize", after: "RSpec.configure do |config|")
```

You can use regular Ruby code inside these methods, and I'm sure if you're this far,
you don't need help on the basics of writing methods. Like I said above, however,
the main difference is that all the public methods will run, so if you want certain
methods to run only when they are explicitly called, make them private.

### Step 3 - Create a Test

Yes, I know best practices say to test first. I agree with this sentiment, but it's
often hard to write the tests first when you are building a new structure for the very
first time. It's tough to know what to test for or how to create the test when you
don't know what the basic structure of what you're trying to build will look like.

That being said, I'll look the other way this time. Write your tests first in the future.

This example will be done in RSpec.

I highly recommend using [Generator Spec](https://github.com/stevehodgkiss/generator_spec)
to help with testing. Just add `s.add_development_dependency "generator_spec"` to
your `gemspec` file.

The spec file placement is much simpler. Just create `task_generator_spec.rb` inside
your `spec` folder. In our case, the `install_generator_spec.rb` file looks like this:

``` ruby
require 'spec_helper'
require 'generator_spec'
require 'generators/smashing_documentation/install_generator'
RSpec.describe TacoTuesday::Generators::InstallGenerator, type: :generator do
  it "serves Tacos to the user every Tuesday" do
    run_generator
    expect(User).to receive(:taco_delivery)
  end
```

Since we're not in Rails anymore, we have a few `require` lines. The first should be obvious.
The second should only be used if you're using the `Generator Spec` gem. We also
need to include the generator as it is not included automatically.

Below that, it should look like standard RSpec. You'll need to specify the modules before
the generator class that's being tested. The `run_generator` helper is provided by
`Generator Spec`, and does exactly that. There are other helpers available, but this
is by far the most useful. From here, you'll just write your tests as you would with
any other project.

### Conclusion

So, that's about it. Looking over it now, it seems crazy that it took an entire
8 hour day to gather this information and get my first generator up and tested.
Like I said, a lot of the information was scattered, and searching for 'rspec generator
tests' on Google turned up a lot of results about generating RSpec tests in Rails.
Hopefully this will help someone else and save them some time and headache. I know
it would have been helpful to me last week.
