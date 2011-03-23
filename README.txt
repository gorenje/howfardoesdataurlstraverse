DataURLs.txt does not traverse down far enough
----------------------------------------------

Simple example of DataURLs.txt not containing resources that are further
down than one directory.

The Resource directory (those marked with '*' are included in dataURLs.txt):

Resources
  spinner.gif *
  DirOne/
    spinner.gif *
    DirTwo/
      spinner.gif
      DirThree/
        spinner.gif

This means that all images that are too far down, will get requested from the server
instead of being loaded from the dataURLs.txt. This isn't an issue if you have a fast
server and not many requests ;)

Reproduce
---------

prompt> jake release

prompt> less Build/Release/howfardoesdataurlstraverse/Browser.environment/dataURLs.txt

