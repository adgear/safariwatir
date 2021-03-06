require 'rubygems'
require 'rake'

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "safariwatir"
    gem.summary = %q{Automated testing tool for web applications.}
    gem.description = %q{WATIR stands for "Web Application Testing in Ruby".  See WATIR project for more information.  This is a Safari-version of the original IE-only WATIR.}
    gem.email = %q{dave@obtiva.com}
    gem.homepage = %q{http://safariwatir.rubyforge.org/}
    gem.authors = ["Dave Hoover", "Tom Copeland", "François Beausoleil"]

    # Skip the files, since Bundler doesn't support submodules yet
    gem.test_files = []

    gem.add_development_dependency "rspec", ">= 1.2.9"
    gem.add_dependency(%q<rb-appscript>, ">= 0.5.3")
  end
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end

namespace :gemspec do
  task :generate => "submodules:ensure"
end

namespace :submodules do
  task :ensure do
    unless File.file?("spec/watirspec/LICENSE")
      raise "Missing specs: run rake submodules:update"
    end
  end

  task :update do
    sh "git submodule init"
    sh "git submodule update"
  end
end

require 'spec/rake/spectask'
Spec::Rake::SpecTask.new(:spec) do |spec|
  spec.libs << 'lib' << 'spec'
  spec.spec_files = FileList['spec/**/*_spec.rb']
end

Spec::Rake::SpecTask.new(:rcov) do |spec|
  spec.libs << 'lib' << 'spec'
  spec.pattern = 'spec/**/*_spec.rb'
  spec.rcov = true
end

task :spec => :check_dependencies

task :default => :spec

require 'rake/rdoctask'
Rake::RDocTask.new do |rdoc|
  version = File.exist?('VERSION') ? File.read('VERSION') : ""

  rdoc.rdoc_dir = 'rdoc'
  rdoc.title = "safariwatir #{version}"
  rdoc.rdoc_files.include('README*')
  rdoc.rdoc_files.include('lib/**/*.rb')
end
