# What is logging and why do we like it?
A program log is a set of text files (or streams) that note what the program is doing and when.  These are extremely useful for monitoring the health of an ongoing application or for investigating unexpected errors.

## Can you be more specific?

Cool things you can figure out with logs:

* What was the program doing yesterday at 4:57 p.m. (e.g. the time right before this end user sent in a bug report via email)
* How long does the front page take to load on Monday mornings vs Friday nights?
* How many people looked at this particular product page last week?

# Can you show me a simple Ruby program that writes to a log?

Sure!

# nlog.rb

```rb
require "logger"

# build a persistent logger that we can send stuff to at will
def logger
  @_logger ||= Logger.new("nicole.log")
end

# sample command that would be hard to figure out if it wasn't logged
# note: this is going to die
def probably_broken_command

  # add a WARNING level line to the log (these are more important and not often filtered out)
  logger.warn "About to execute this probably broken command"

  # let's do some math and return the value of x so that main can print it
  x = 0
  x = x + 5
  x = x * 2

  raise "Oh man totally broken, program dies now"

  logger.info "Finishing probably broken command"

  return x
end

# set up a logger, do some math, exit gracefully (or will we!?)
def main
  # add a DEBUG line to the log (these get noisy and are often filtered out)
  logger.debug("program starting here")

  sleep 5 # wait 5 seconds

  # execute probably_broken_command and store its results
  results = probably_broken_command

  # print the stored results to the screen
  puts results

  logger.debug("program ending here")
end

# run the main function as defined above
main
```

## Cool!  What happens when you run that program?

```rb
# check the current time
daniel@hubertus-bigend ~> date
Wed Mar 11 16:07:36 CDT 2015

# run our program, see it die with an error message
daniel@hubertus-bigend ~> ruby ./nlog.rb
./nlog.rb:18:in `probably_broken_command': Oh man totally broken, program dies now (RuntimeError)
    from ./nlog.rb:31:in `main'
    from ./nlog.rb:38:in `<main>'

# read the just-crashed program's log from a text file and see it's debug and warn lines
# notice that the log stops right before "hey y'all watch this" and the program dies before it
# could log anything else.  Useful clue!
daniel@hubertus-bigend ~> cat ./nicole.log 
# Logfile created on 2015-03-11 16:07:41 -0500 by logger.rb/44203
D, [2015-03-11T16:07:41.382372 #27947] DEBUG -- : program starting here
W, [2015-03-11T16:07:46.382623 #27947]  WARN -- : About to execute this probably broken command
```
