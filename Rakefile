# encoding: utf-8
require 'rake'
require 'tempfile'
require 'rake/clean'
require 'yaml'

task default: [
  :clean,
  :build
]

def done(msg)
  puts msg + "\n\n"
end

desc 'Delete _site directory'
task :clean do
  sh 'rm','-rf', '_site'
  done 'Site directory deleted successfully.'
end

desc 'Start web server to preview site'
task :preview do
  sh 'jekyll', 'serve', '--watch', '--drafts', '--port', ENV.fetch('PORT', '4000')
  done 'Web server started.'
end

desc 'Executing all tests.'
task :test do
  done 'All tests executed successfully.'
end

desc 'Creating artifacts.'
task :artifacts do
  done 'All artifacts built successfully.'
end

desc 'Publishing application on aws'
task :deploy do
  if File.exist? '_site'
    fail 'Push to s3 is failed.' unless system('s3_website', 'push')
  else
    done 'Site has not been built yet (run "rake build" first)'
  end
end

desc 'Build site'
task :build do
  if File.exist? '_site'
    done 'Jekyll site already exists in _site (run "rake clean" first)'
  else
    fail 'Jekyll failed' unless system('jekyll', 'build')
  end
end

desc 'Print environment variables'
task :print_env do
  puts ENV.to_h.to_yaml
end