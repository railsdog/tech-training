# What is JRuby?

JRuby is a ruby interpreter built on top of Java.

# What is a ruby interpreter?

Ruby is a programming language.  A simple ruby file might look like the following `hello-world.rb` example:

```rb
# hello-world.rb

puts "Hello, World!"
puts 2 * 2
```

`ruby` is also a programming language interpreter. You can execute the `ruby` interpreter and it will process a Ruby source code file like so:

```sh
 ruby hello-world.rb
 Hello, world!
 4
```

The default `ruby` interpreter is itself a program that is largely written in the C programming language.
JRuby is a Ruby interpreter written in the Java programming language:

```sh
 jruby hello-world.rb
 Hello, world!
 4
```

# Why is there an alternate Ruby interpeter written in Java?

Two major reasons:

1) Java can be faster for certain workloads

2) JRuby can integrate some Java tools that make certain solutions easier

# Why did we use JRuby for this project?

Usually JRuby is selected for projects that are either integrating with a large Java codebase (i.e. the client is a large company that loves Java) or the project has well-known scalability needs that JRuby might help out with.

# Why would you ever *not* use JRuby if it's faster?

Since C Ruby (also known as MRI Ruby) is the default that most Rubyists have always used, there are many important Ruby code libraries written for C Ruby that do not run in JRuby.  This can mean more work rewriting those tools or learning JRuby substitutes.

Equally important is the fact that JRuby program management and tooling doesn't look quite like C Ruby tooling.  Your programmers and sysadmins may have to read further or traing more to learn how to do something in JRuby that they already knew how to do in C Ruby.

JRuby is also slower for very small programs.  C Ruby can start and run and finish in a half a second for a really simple program.  JRuby often takes several seconds just to get started, but then it might be faster once it gets going.  This is ideal for long-running server applications like Spree.
