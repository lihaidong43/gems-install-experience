##Build native extension ##
**record some experience when install some gems on the Windows**
###libv8###

will occupy error like this
 

> `gem install libv8`
> `C:/Ruby193/lib/ruby/gems/1.9.1/gems/libv8-3.16.14.3/ext/libv8/builder.rb:58:in setup_python!': libv8 requires python 2 to be installed in order to build, but it is currently not available (RuntimeError)`


and then you just add **--with-system-v8** argument after gem install libv8,etc
>
 `gem install libv8  -- --with-system-v8`

###puma###

> `gem install puma`
> `Gem::Installer::ExtensionBuildError: ERROR: Failed to build gem native extension.
C:/Ruby193/bin/ruby.exe extconf.rb
creating Makefile
make
generating puma_http11-i386-mingw32.def
compiling http11_parser.c
ext/http11/http11_parser.rl: In function 'puma_parser_execute':
ext/http11/http11_parser.rl:111:3: warning: comparison between signed and unsigned integer expressions
compiling io_buffer.c
io_buffer.c: In function 'buf_to_str':
io_buffer.c:118:3: warning: pointer targets in passing argument 1 of 'rb_str_new' differ in signedness
c:/Ruby193/include/ruby-1.9.1/ruby/intern.h:661:7: note: expected 'const char *' but argument is of type 'uint8_t *'
compiling mini_ssl.c
In file included from mini_ssl.c:2:0:
c:/Ruby193/include/ruby-1.9.1/ruby/backward/rubyio.h:2:2: warning: #warning use "ruby/io.h" instead of "rubyio.h"
mini_ssl.c:3:25: fatal error: openssl/bio.h: No such file or directory
compilation terminated.
make: *** [mini_ssl.o] Error 1`

puma dependent on openssl ,you need specify openssl dir when install puma gem,but first you need download openssl [http://packages.openknapsack.org/openssl/openssl-1.0.0k-x86-windows.tar.lzma](http://packages.openknapsack.org/openssl/openssl-1.0.0k-x86-windows.tar.lzma "openssl-x86-windows") when your devkit's version is 32bit,or you need download [http://packages.openknapsack.org/openssl/openssl-1.0.0k-x64-windows.tar.lzma](http://packages.openknapsack.org/openssl/openssl-1.0.0k-x64-windows.tar.lzma "openssl-x64-windows") when your devkit's version is 64bit. you can also download it from openssl direcotry in this repository.
> gem install puma -- --with-opt-dir=path/to/openssl

###therubyracer###
[https://github.com/takewo/therubyracer_windows](https://github.com/takewo/therubyracer_windows)



###fix the invalid bytes sequence in utf-8###

namespace :assets do
  
  task  :check => :environment do
    paths = ["app/assets", "lib/assets", "vendor/assets"]
    
    paths.each do |path|
      dir_path = Rails.root + path
      
      if File.exists?(dir_path)
        dir_files = File.join(dir_path, "**")
        
        Dir.glob(dir_files + "/**.{js,css}").each do |file|
        
            # make sure we're not trying to process a directory
            unless File.directory?(file)
              # read the file and check its encoding
              data = File.read(file)              
              unless data.valid_encoding?
                puts "#{ file } does not have valid encoding!"
              end
            end
        
        end # end Dir.glob
        
      end #end File.exists
    end # end paths.each
    
  end
  
end


