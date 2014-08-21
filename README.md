gems install experience on Windows
=======================
libv8
==
   when execute 'gem install libv8' on command line ,it will have some error just like :
   C:/Ruby193/lib/ruby/gems/1.9.1/gems/libv8-3.16.14.3/ext/libv8/builder.rb:58:in `setup_python!': libv8 requires python 2 to be installed in order to build, but it is currently not available (RuntimeError)
   and then you can install it with **' gem install libv8 -v '3.11.8.17' -- --with-system-v8'**

puma
==
   when you install puma gem on windows,just like 'gem install puma' ,it have some error like:
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
make: *** [mini_ssl.o] Error 1

  above error that remind to specify openssl ,you should download openssl package and specify it when install it,
  **gem install puma -v '2.5.0' -- --with-opt-dir=path/to/openssl**
  ps: if you devkit is x86 version ,that must use x86 ,or will occupy error also
  

   

   



Record some gems install experience for building native extension
