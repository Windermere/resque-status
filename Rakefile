$LOAD_PATH.unshift './lib'

require 'rubygems'
require 'rake'
require 'resque-status'
require 'resque/tasks'

require "bundler/gem_tasks"

module Bundler
  class GemHelper
    def rubygem_push(path)
      gem_server_url = ENV['GEM_SERVER_URL']
      sh("gem inabox '#{path}' --host #{gem_server_url}")
      Bundler.ui.confirm "Pushed #{name} #{version} to #{gem_server_url}"
    end
  end
end

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "resque-status"
    gem.version = Resque::Plugins::Status::VERSION
    gem.summary = %Q{resque-status is an extension to the resque queue system that provides simple trackable jobs.}
    gem.description = %Q{resque-status is an extension to the resque queue system that provides simple trackable jobs. It provides a Resque::Plugins::Status::Hash class which can set/get the statuses of jobs and a Resque::Plugins::Status class that when included provides easily trackable/killable jobs.}
    gem.email = "aaron@quirkey.com"
    gem.homepage = "http://github.com/quirkey/resque-status"
    gem.rubyforge_project = "quirkey"
    gem.authors = ["Aaron Quint"]
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

require 'rake/testtask'
Rake::TestTask.new(:test) do |test|
  test.libs << 'lib' << 'test'
  test.pattern = 'test/**/test_*.rb'
  test.verbose = true
end

begin
  require 'rcov/rcovtask'
  Rcov::RcovTask.new do |test|
    test.libs << 'test'
    test.pattern = 'test/**/test_*.rb'
    test.verbose = true
  end
rescue LoadError
  task :rcov do
    abort "RCov is not available. In order to run rcov, you must: sudo gem install spicycode-rcov"
  end
end

task :test

task :default => :test

begin
  require 'rdoc/task'
rescue LoadError
  require 'rdoc/rdoc'
  require 'rake/rdoctask'
  RDoc::Task = Rake::RDocTask
end

RDoc::Task.new(:rdoc) do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "resque-status #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
