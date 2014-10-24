# Windows Install Guide

Install Ruby and Rails via RailsFTW:

    http://railsftw.bryanbibat.net/

Select the big red button that says "Download Latest", and when the download is finished, run the `rails-ftw-[some_numbers].exe` file.

The default install options are good, you should not need to change anything. The only thing to watch out for is that the "Install Location" part does not contain any spaces. Ninety-nine percent of the time, it should not have any by default.

### Git via msysgit

Next, we need the 'msysgit' package from a Google Code repository:

    http://msysgit.github.io/

Download the most recent version (first in the list). As of October 2014, it will be named `Git-1.9.4-preview[some_numbers].exe`. When it is done downloading, run the file and install with the default options.

When it is done installing, open your start menu (or start screen in Windows 8) and type "bash" in the text box. An option called "Git Bash" should come up. Run that program.

This is your terminal. You will be using this to enter all sorts of commands tomorrow. To make sure everything worked properly, type:

    ruby -v

And hit enter. The next line should show something that starts with "ruby 2.1", possibly with more numbers afterward, a date, and the word "mingw32". Those are all completely fine.

Next run the command, being careful to use the exact spaces and hyphens:

    gem install bundler --no-ri --no-rdoc

And it should say "Successfully installed bundler-1.5.3" and another line "1 gem installed". If that has worked out, you're all set!

## ImageMagick for Image Uploads on Windows

In order to use various image-related tools for one of our Explorations tomorrow, you will need to install three extra tools: The Ruby DevKit, ImageMagick and a gem called rmagick.

### Ruby DevKit

First head over to

    http://rubyinstaller.org/downloads/

and in the left-hand column, under the **Devlopment Kit** section, select the download for "Ruby 2.0 and 2.1" for 32-bit or 64-bit depending on your version of Windows. They should be named "DevKit-mingw64-[lots of numbers]-sfx.exe". Run that and extract it to a location *with no spaces in the name* (here we will use C:\Ruby\DevKit). Then in your "Git Bash" window (or open a new one), you will want to run

```bash
$ cd C:\Ruby\DevKit
$ ruby dk.rb init
```

which will set up the DevKit for use in our next steps.

### ImageMagick

