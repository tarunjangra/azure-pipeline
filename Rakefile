# encoding: utf-8

require 'rubygems'
require 'rake'
require 'tempfile'
require 'rake/clean'
require 'net/http'
require 'rubocop/rake_task'

task default: [
  :clean,
  :build,
  :test,
  :artifacts
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
    sh 's3_website', 'push'
    fail 'Push to s3 is failed.' unless SCHILD_STATUS.success?
    done 'Site has been published to S3.'
  else
    done 'Site has not been built yet (run "rake build" first)'
  end
end

desc 'Build site'
task :build do
  if File.exist? '_site'
    done 'Jekyll site already exists in _site (run "rake clean" first)'
  else
    sh 'jekyll', 'build'
    fail 'Jekyll failed' unless $CHILD_STATUS.success?
    done 'Jekyll site generated without issues'
  end
end