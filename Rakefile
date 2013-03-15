require 'yaml'

config_file = '_config.yml'
config = YAML.load_file(config_file)

env = ENV['env'] || 'stage'

task :deploy do
  command = "rsync -avz --delete "
  command << "-e 'ssh -p #{config['environments'][env]['remote']['port']}' " unless config['environments'][env]['remote']['port'].nil?
  command << "#{config['destination']}/ #{config['environments'][env]['remote']['connection']}:#{config['environments'][env]['remote']['path']}"
  sh command
end

desc "Start a new post"																																																																		
task :new_post, :title do |t, args|																																																												
 args.with_defaults(:title => 'My New Post')																																																							
 title = args.title																																																																				
 filename = "_posts/#{Time.now.strftime('%Y-%m-%d')}-#{title.downcase.gsub(/&/,'and').gsub(/[,'":\?!\(\)\[\]]/,'').gsub(/[\W\.]/, '-').gsub(/-+$/,'')}.md"
 puts "Creating new post: #{filename}"																																																										
 open(filename, 'w') do |post|																																																														
   system "mkdir -p _posts";																																																															
   post.puts "---"																																																																				
   post.puts "layout: post"																																																																
   post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""																																																			
   post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"																																																
   post.puts "published: false"																																																														
   post.puts "---"																																																																				
 end																																																																											
end																																																																												