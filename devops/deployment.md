# What is 'deployment' exactly?

Deployment is taking a new version of a program which was developed on a laptop or workstation and pushing that new version to a staging or production server.

# Why?

Getting from "this looks good on my machine" to "other people can see and interact with this software" is where the rubber meets the road in software development.

# How?

At Railsdog we'll usually have our devops team create a staging server and set up the basic tooling to make each unique application deployable.

# What does it look like?

```sh
cap staging deploy
```

A simple `cap deploy` command will use Capistrano to connect to the remote server, pull in your latest source code from Github, and set it up on the staging (or production) server.  Once that's done we'll usually automatically run any follow-up tasks that need running such as `rake db:migrate` (e.g. bring the database up to date with our latest design).  Once that's done an end user should be able to connect to the staging server and try out the latest changes.
