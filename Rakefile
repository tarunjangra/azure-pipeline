# encoding: utf-8
require 'rake'
require 'rake/clean'
require 'yaml'
require 'redcloth'
require 'stringex'

POSTS_DIR = '_posts'
BUILD_DIR = '_site'

CLEAN.include BUILD_DIR

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
  fail 'Jekyll failed' unless system('jekyll', 'build')
end

desc 'Print environment variables'
task :print_env do
  puts ENV.to_h.to_yaml
end

desc 'Create a new draft'
task :new_draft, :title do |t, args|
  title = args[:title] || 'New Draft'
  filename = File.join('_drafts', "#{title.to_url}.md")

  puts "==> Creating new draft: #{filename}"
  open(filename, 'w') do |f|
    f << "---\n"
    f << "layout: post\n"
    f << "title: \"#{title.to_html(true)}\"\n"
    f << "comments: false\n"
    f << "categories:\n"
    f << "---\n"
    f << "\n"
    f << "Add awesome content here.\n"
  end
end

desc 'Create a new post'
task :new_post, :title do |t, args|
  title = args[:title] || 'New Post'
  timestamp = Time.now.strftime('%Y-%m-%d')
  filename = File.join(POSTS_DIR, "#{timestamp}-#{title.to_url}.md")

  puts "==> Creating new post: #{filename}"
  open(filename, 'w') do |f|
    f.write "---\n"
    f.write "layout: post\n"
    f.write "title: \"#{title.to_html(true)}\"\n"
    f.write "categories:\n"
    f.write "---\n"
    f.write "\n"
    f.write "Add awesome post content here.\n"
  end
end

desc 'Create a new page'
task :new_page, :title do |t, args|
  title = args[:title] || 'New Page'
  filename = File.join("#{title.to_url}.md")

  puts "==> Creating new page: #{filename}"
  open(filename, 'w') do |f|
    f.write "---\n"
    f.write "layout: page\n"
    f.write "title: \"#{title.to_html(true)}\"\n"
    f.write "---\n"
    f.write "\n"
    f.write "Add awesome page content here.\n"
  end
end