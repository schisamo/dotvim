if ENV['OS'] =~ /Windows.*/
  vimdir = File.expand_path("C:/Program Files/Vim/vim72")
  vimrc  = File.expand_path("~/_vimrc")
else
  vimdir = File.expand_path("~/.vim")
  vimrc  = File.expand_path("~/.vimrc")
end

desc "Install vim configuration"
task :install do
  sh "mkdir -p #{vimdir}" unless FileTest.directory?("#{vimdir}")
  puts "Installing to #{vimdir}"
  sh "tar -cpf - * | (cd #{vimdir} && tar -xpf -)"
  puts "Creating link for #{vimrc}"
  File.symlink("#{vimdir}/vimrc", vimrc) unless File.symlink?(vimrc)
end

desc "Install vim configuration on Windows"
task :install_windows do
  puts "Installing to #{vimdir}"
  Dir.entries(".").each do |d|
    if FileTest.directory?(d) && d =~ /^[a-z]/
      Dir.entries(d).each do |source|
        next if FileTest.directory?(source)
        copy("#{d}/#{source}", "#{vimdir}/#{d}")
      end
    end
  end
  copy("vimrc", "#{vimrc}")
end

