require 'rake/testtask'

desc 'Default: run unit tests.'
task :default => [:create_database, :test]

desc 'Test the will_paginate plugin.'
Rake::TestTask.new(:test) do |t|
  t.pattern = 'test/**/*_test.rb'
  t.libs << 'test'
end

namespace :test do ||
  desc 'Test only Rails integration'
  Rake::TestTask.new(:rails) do |t|
    t.pattern = %w[test/finder_test.rb test/view_test.rb]
    t.libs << 'test'
  end

  desc 'Test only ActiveRecord integration'
  Rake::TestTask.new(:db) do |t|
    t.pattern = %w[test/finder_test.rb]
    t.libs << 'test'
  end
end

desc 'Create necessary databases'
task :create_database do |variable|
  case ENV['DB']
  when 'mysql', 'mysql2'
    `mysql -e 'create database will_paginate;'`
    abort "failed to create mysql database" unless $?.success?
  when 'postgres'
    `psql -c 'create database will_paginate;' -U postgres`
    abort "failed to create postgres database" unless $?.success?
  end
end
