!SLIDE
## Running jruby-complete directly

!SLIDE commandline incremental

    $ java -jar jruby-complete-1.4.0.jar

    $ java -jar jruby-complete-1.4.0.jar -e "puts 'Hello'"
      Hello

!SLIDE commandline

    $ java -Xmx500m -Xss1024k -jar jruby-complete-1.4.0.jar -e "puts 'Hello'"
      Hello

!SLIDE commandline

# irb

    $ java -Xmx500m -Xss1024k -jar jruby-complete-1.4.0.jar -S jirb
      irb(main):001:0> puts "Hello"
      Hello
      => nil

!SLIDE

# Rake tasks

    @@@ ruby
    JRUBY_COMPLETE = "jruby-complete-1.4.0.jar"
    JRUBY = "java -Xmx500m -Xss1024k -jar #{JRUBY_COMPLETE}"

!SLIDE

    @@@ ruby
    namespace :jruby do
      desc "Run JRuby help"
      task :help do
        sh %+#{JRUBY} --help+
      end
    
      desc "Run any command with JRuby"
      task :run do
        sh %+#{JRUBY} -e '#{ENV["cmd"]}'+
      end
    end

!SLIDE commandline

    $ rake jruby:run cmd='puts "Hello"'
      Hello
