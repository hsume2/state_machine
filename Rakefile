require 'bundler/setup'
require 'bundler/gem_tasks'
require 'rake/testtask'

desc 'Default: run all tests.'
task :default => :test

Rake::TestTask.new(:test) do |t|
  t.libs << 'lib'
  t.test_files = ENV['INTEGRATION'] ? Dir["test/unit/integrations/#{ENV['INTEGRATION']}_test.rb"] : Dir['test/{functional,unit}/*_test.rb'] + ['test/unit/integrations/base_test.rb']
  t.verbose = true
end

begin
  require 'rcov/rcovtask'
  namespace :test do
    desc "Test the #{spec.name} plugin with Rcov."
    Rcov::RcovTask.new(:rcov) do |t|
      t.libs << 'lib'
      t.test_files = spec.test_files
      t.rcov_opts << '--exclude="^(?!lib/)"'
      t.verbose = true
    end
  end
rescue LoadError
end

load File.dirname(__FILE__) + '/lib/tasks/state_machine.rake'
