begin
  require 'bundler/setup'
rescue LoadError
  puts 'You must `gem install bundler` and `bundle install` to run rake tasks'
end

require 'rdoc/task'

RDoc::Task.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title    = 'FrontEndBuilds'
  rdoc.options << '--line-numbers'
  rdoc.rdoc_files.include('README.rdoc')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

begin
  require 'rspec/core/rake_task'
  RSpec::Core::RakeTask.new(:spec)
  task :default => :spec
rescue LoadError
  # no rspec available
end

namespace :admin do
  task :build do
    copy_files = {
      'admin/dist/assets/admin.css' => 'app/assets/stylesheets/front_end_builds/admin.css',
      'admin/dist/assets/vendor.css' => 'app/assets/stylesheets/front_end_builds/vendor.css',
      'admin/dist/assets/admin.js' => 'app/assets/javascripts/front_end_builds/admin.js',
      'admin/dist/assets/vendor.js' => 'app/assets/javascripts/front_end_builds/vendor.js',
    }

    Dir.chdir('admin') do
      sh 'ember build  --environment production'
    end

    copy_files.each do |source, dest|
      FileUtils.cp(source, dest)
    end
  end
end

APP_RAKEFILE = File.expand_path("../spec/dummy/Rakefile", __FILE__)
load 'rails/tasks/engine.rake'


Bundler::GemHelper.install_tasks
