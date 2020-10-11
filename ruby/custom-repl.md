# Custom REPL

```ruby
#!/usr/bin/ruby

# Toy script used to generate REPLs for arbitrary tasks or commands:
#
# > repl.rb nslookup %s
# > repl.rb df -h %s
#
# Is possible to enable readline functionality by wrapping this using rlwrap:
#
# > rlwrap ruby repl.rb nslookup %s
#
class Repl
  def show_usage
    puts "Usage: repl <command> <argument> %s <argument> ..."
  end

  def run_from_args
    if valid_args?
      command = ARGV.join(" ")
      run(command)
    else
      show_usage
    end
  end

  def valid_args?
    ARGV.length > 0 && ARGV.include?("%s")
  end

  def run(command)
    loop do
      print "> "
      arguments = STDIN.gets.chomp
      break if arguments == 'exit'

      puts `#{command.gsub("%s", arguments)}`
    end
  end
end

Repl.new.run_from_args
```
