# What is git?

Git is a revision control system.  It provides us with a way to track the full
lifecycle of a text-based document (primarily Ruby code files) one change at a time.

## How do you track revisions to a text file?

Say you have a twenty line text file and someone wants to make a copy edit to a single word
in line three.  They can make that change on their machine and then "commit" the change via git
with an informative message like 'corrected spelling of banana'.  That commit can then be shared with
the rest of the team (often by being reshared through GitHub) so that everyone else can apply that
change and see the updated file on their machines.

The interesting thing about how Git works is that you don't have to send a full copy of the file
along with each change, you just send the change itself and Git stitches it together to show the difference.

I'll need to update this with a lot more information some day.


## What's a pull request?
