require 'rake/clean'

CLEAN.include('*~')
FILES_TO_TIDY = [ '*.xml', '*.rb', 'Rakefile' ]

desc "Set permissions"
task :permissions do
  system "find . -type f -print0 | xargs -0 chmod 644"
  system "find . -type d -print0 | xargs -0 chmod 755"
end

desc "Check for valid XML and Ruby"
task :check do
  puts 'Checking XML recipes'
  Dir.glob('*.xml') do |f|
    # puts "Checking #{f}"
    system "xmllint --noout '#{f}'"
  end
  puts 'Checking ruby scripts'
  system "find . -name '*.rb' -print0 | xargs -0 ruby -c"
end

desc "Tidy lineendings and empty spaces"
task :tidy do
  system "find . -name '*.xml' -print0 | xargs -0 fromdos"
  FILES_TO_TIDY.each do |f|
    system "find . -name '#{f}' -print0 | xargs -0 sed -i 's/[ \t]*$//g'"
  end
end

desc "Create package list"
task :package_list do
  puts "TODO: use xgrep or xpath queries instead of this to find variables"
  system %q[ grep name= *.xml | grep -v variable | cut -f2 -d '"' | sort -u | todos > package_list.txt ]
end

desc 'Pull latest source'
task :pull do
  system 'git pull'
  system 'git submodule update --init --recursive'
end

desc 'Push source'
task :push do
  system 'git push'
end

task default: [:clean, :permissions, :tidy, :check ]
