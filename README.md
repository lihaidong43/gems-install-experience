##Build native extension when install some gems on the Windows##
**record some experience**
###libv8###

will occupy error like this
 

> gem install libv8
> `C:/Ruby193/lib/ruby/gems/1.9.1/gems/libv8-3.16.14.3/ext/libv8/builder.rb:58:in setup_python!': libv8 requires python 2 to be installed in order to build, but it is currently not available (RuntimeError)`


and then you just add **--with-system-v8** argument after gem install libv8,etc
>
 `gem install libv8  -- --with-system-v8`

###puma###
