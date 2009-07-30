if ENV['OS'] =~ /Windows.*/
  winarc = ENV['PROCESSOR_ARCHITECTURE'] =~ /x86/ ? " (x86)" : ''
  vimdir = File.expand_path("C:/Program Files#{winarc}/Vim/vim72")
  vimrc  = File.expand_path("~/_vimrc")
else
  vimdir = File.expand_path("~/.vim")
  vimrc  = File.expand_path("~/.vimrc")
end

desc "Install vim configuration"
task :install do
  puts "Installing to #{vimdir}"
  if ENV['OS'] =~ /Windows.*/
    Dir.entries(".").each do |d|
      if FileTest.directory?(d) && d =~ /^[a-z]/
        Dir.entries(d).each do |source|
          next if FileTest.directory?(source)
          copy("#{d}/#{source}", "#{vimdir}/#{d}")
        end
      end
    end
    copy("vimrc", "#{vimrc}")
  else
    sh "mkdir -p #{vimdir}" unless FileTest.directory?("#{vimdir}")
    sh "tar -cpf - * | (cd #{vimdir} && tar -xpf -)"
    puts "Creating link for #{vimrc}"
    File.symlink("#{vimdir}/vimrc", vimrc) unless File.exists?(vimrc)
  end
end

task :default => :install
