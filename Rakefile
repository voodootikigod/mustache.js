require 'rake'
require 'spec/rake/spectask'

task :default => :spec

Spec::Rake::SpecTask.new(:spec) do |t|
  #t.spec_opts = ['--options', "\"#{File.dirname(__FILE__)}/spec/spec.opts\""]
  t.spec_files = FileList['test/*_spec.rb']
end

desc "Run all specs"
task :spec do
end


def template_generator(template, options={})
  name_prefix = options[:name_prefix] || ""
  
  `mkdir -p build; mkdir -p build/#{template}`
  `cat pkg/#{template}.tpl.pre mustache.js pkg/#{template}.tpl.post > build/#{template}/#{name_prefix}mustache.js`
  print "Done, see ./build/#{template}/#{name_prefix}mustache.js\n"
end


task :commonjs do
  print "Packaging for CommonJS\n"
  template_generator("commonjs")
end

task :jquery do
  print "Packaging for jQuery\n"
  template_generator("jquery", :name_prefix=>"jquery.")
end


task :dojo do
  print "Packaging for dojo\n"
  # handle dojo with a bit of love
  path = %w(build dojo dojox string)
  prefix = ""
  path.each{|p|
    `mkdir -p #{prefix}#{p}`
    prefix += "#{p}/"
  }
  `cat pkg/dojo.tpl.pre mustache.js pkg/dojo.tpl.post > build/dojo/dojox/string/mustache.js`
  print "Done, see ./build/dojo/dojox/string/mustache.js | Include using dojo.require('dojox.string.mustache'); \n"
end


task :build do
  ["jquery", "commonjs", "dojo"].each{|t|
    Rake::Task[t].execute
  }
end


task :clean do
  `for file in \`cat .gitignore\`; do rm -rf $file; done`
end



