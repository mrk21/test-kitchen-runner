# test-kitchen-runner

This is Docker image for running [test-kitchen](https://github.com/test-kitchen/test-kitchen "test-kitchen/test-kitchen") script. This supports Ruby 2.2 with Bundler, latest Ansible and latest Docker. If you want to use Docker, it needs `--privileged=true` option when this image running.

## An example

If the project is used with [kitchen-ansible](https://github.com/neillturner/kitchen-ansible "neillturner/kitchen-ansible") and [kitchen-docker](https://github.com/portertech/kitchen-docker):

```
your_project
├── .kitchen.yml
├── Gemfile
├── Rakefile
├── site.yml
└── test
    └── integration
        └── default
...
```

Gemfile:

```ruby
source "https://rubygems.org"

gem 'test-kitchen'
gem 'kitchen-ansible'
gem 'kitchen-docker'
gem 'docker'

group :integration do
  gem 'serverspec'
  gem 'specinfra'
end
```

Rakefile:

```ruby
begin
  require "kitchen/rake_tasks"
  Kitchen::RakeTasks.new
rescue LoadError
  puts ">>>>> Kitchen gem not loaded, omitting tasks" unless ENV["CI"]
end
```

If you want to run the tests of the above project, you will execute the commands listed below:

```bash
$ bundle install --path=vendor/bundle
$ bundle exec rake kitchen:all
```
