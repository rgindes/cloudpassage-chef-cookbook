require 'rake'
require 'rspec'

namespace :style do
  require 'rubocop/rake_task'
  desc 'Run rubocop style checks'
  RuboCop::RakeTask.new(:ruby)
  require 'foodcritic'
  desc 'Run foodcritic style checks'
  FoodCritic::Rake::LintTask.new(:chef)
end

namespace :spec do
  require 'rspec/core/rake_task'
  desc 'Run rspec tests'
  RSpec::Core::RakeTask.new(:spec)
end

namespace :integration do
  require 'kitchen/cli'
  task :vagrant do
    desc 'Run kitchen-vagrant tests'
    ENV['KITCHEN_YAML'] = '.kitchen.yml'
    Kitchen::CLI.new([], concurrency: 2, destroy: 'always').test
  end
  task :ec2 do
    desc 'Run kitchen-vagrant tests'
    ENV['KITCHEN_YAML'] = '.kitchen.ec2.yml'
    Kitchen::CLI.new([], concurrency: 2, destroy: 'always').test
  end
end

desc 'Runs all style checks'
task style: ['style:chef', 'style:ruby']

desc 'Runs spec tests'
task spec: ['spec:spec']

desc 'Runs all integration tests using kitchen-vagrant and kitchen-ec2'
task integration: ['integration:vagrant', 'integration:ec2']
task travis: [:style, :spec]

task default: [:style, :spec, :integration]
task ec2: [:style, :spec, :integration:ec2]
