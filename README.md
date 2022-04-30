# Automate Waking Up Your Heroku Server

Free heroku servers like to go to sleep every 60 minutes unless you pay them money (how dare they). This can be annoying because projects will take a while to wake up if no ones been there in a while and this can look less than great to recruiters etc. You know all this.

There are services that will ping your heroku projects every hour to keep them awake but they can feel sketchy and be impossible or difficult to turn off. Which is an issue if you're doing it too much and run out of dyno hours. Then all your projects shut down for the rest of the month.

You can write your own mini application to keep your projects awake without relinquishing precious control to other services though and learn a little bash and browser automation along the way.

These instructions are for bash but will be similar in powershell or zsh.

## TL;DR
  - Heroku servers go to sleep every hour
  - There are semi-sketchy services that keep them awake for you
  - You can write your own command line script to do this
  - Put [this code](#write-that-code) in a bash script file and run it

## Setup:
  - These instructions are for bash but powershell / zsh should be similar
  - Make sure your Google Chrome is up-to-date

## Write the Code

### Make a Bash File (.sh)

Make a new file anywhere you want on your computer called heroku.sh. You can do this from the command line if you want.

```bash
  $ touch heroku.sh
```

Note that .sh indicates this is a bash script if you aren't using bash. 

### Open the File

4. Open that file up so you can write in it. You can do this in an IDE like VSCode but you aren't going to be writing much code so maybe practice opening it in a command line text editor just for fun like nano, vim or emacs.

```bash
$ nano heroku.sh
```

sidenote: this actually makes a new file if it doesn't exist so you could just skip the previous step technically.

### Write that Code

You can paste this code into your bash file but you might learn more by typing it out. 

Basically this is shell script (specifically bash syntax), meaning it could all be typed directly in your command line and would be valid syntax. We can put shell script into files though to save the trouble of typing things like this out repeatedly or to help if the commands form more complex multi-line scripts.

```bash
while true
do
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --dump-dom https://YOURHEROKUSITE1.com
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --dump-dom https://YOURHEROKUSITE2.com
  # add your other heroku projects here by repeating the above line as many times as you want
  # note that this includes an absolute path that goes inside your Google Chrome application folder
  # this should work for a Mac but make sure that path is valid
  sleep 1700
done
```

Lets break that all down quickly. Remember the the syntax / language here is bash script.

This part (below 👇) just sets up an infinite while loop with a 59 minute (1740 second) pause before repeating the loop.

```bash
while true
do
  # ...
  sleep 1740
done
```

This part (below 👇) uses your Chrome browser in headless mode (meaning no visual browser interface) and requests the DOM information. Thereby waking up the server and keeping it awake for the next hour on heroku's end.

```bash
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --dump-dom https://YOURHEROKUSITE1.com
```

## Using Your New Shell Script

Now all you need to do is let this run in it's own terminal window forever. Or realistically just let it run whenever you have your computer on. For bash users you can run it by typing this directly in your command line and pressing enter. This uses the bash utility to run a bash script written in a .sh file.

```bash
$ bash heroku.sh
```

Now let that run for as long as you want to keep your server awake and open a new command line window or tab for your other tasks.

This will save you dyno hours since you can turn it off during off hours when people are less likely to be checking out your portfolio and will let you remove websites etc so you dont waste free dyno hours on projects that are no longer on your portfolio (someday).


## Problems?

If you encounter issues running this remember Google (or DDG) is your friend. What you are trying to do is open a webpage with a headless browser in the command line and write a while loop in a command line script with a 59 minute delay or pause. You should be able to get something working in any environment if you pop all of that into a search engine. Here's a list of stuff to check though for the tldr crowd.

* update google chrome
* check your google chrome path in the script
* check your project urls
* check to see if you're running bash or zsh etc
* get your google / ddg on


## Bonus Challanges

1. Figure out how to get this script to run in the background (as a daemon) so you dont have to take up a terminal window looking at it.
2. Figure out how to initiate this script automatically every time you open a new terminal / command prompt instance.
3. Figure out how to do this with Puppetmaster or Selenium (more powerful browser automation / webscraping tools)
4. Write your first webscraper for no particular reason!
5. Write a bash script to automate something repetitive!
