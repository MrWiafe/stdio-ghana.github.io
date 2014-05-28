# courtesy of guidance at http://davidensinger.com/

task :default => 'commit_deploy'

desc "Commit _site/"
task :commit do
  puts "\n## Staging modified files"
  puts system("git add -A") ? "Success" : "Failed"
  puts "\n## Committing a site build at #{Time.now.utc}"
  puts system("git commit -m \"Build site at #{Time.now.utc}\"") ? "Success" : "Failed"
  puts "\n## Pushing commits to remote"
  puts system("git push origin source") ? "Success" : "Failed"
end

desc "Deploy _site/ to master branch"
task :deploy do
  puts "\n## Deleting master branch"
  status = system("git branch -D master")
  puts status ? "Success" : "Failed"
  puts "\n## Creating new master branch and switching to it"
  status = system("git checkout -b master")
  puts status ? "Success" : "Failed"
  puts "\n## Forcing the _site subdirectory to be project root"
  status = system("git filter-branch --subdirectory-filter _site/ -f")
  puts status ? "Success" : "Failed"
  puts "\n## Switching back to source branch"
  status = system("git checkout source")
  puts status ? "Success" : "Failed"
  puts "\n## Pushing all branches to origin"
  status = system("git push --all origin")
  puts status ? "Success" : "Failed"
end

desc "Commit and deploy _site/"
task :commit_deploy => [:commit, :deploy] do
end
