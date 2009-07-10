vimdir = File.expand_path("~/.vim")
vimrc  = File.expand_path("~/.vimrc")

desc "Install vim configuration"
task :install do
  sh "mkdir -p #{vimdir}" unless FileTest.directory?("#{vimdir}")
  puts "Installing to #{vimdir}"
  sh "tar -cpf - * | (cd #{vimdir} && tar -xpf -)"
  puts "Creating link for #{vimrc}"
  File.symlink("#{vimdir}/vimrc", vimrc) unless File.symlink?(vimrc)
end

