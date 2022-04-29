# Heroku Slap

Free heroku servers like to go to sleep every 60 minutes unless you pay them money (how dare they). This can be annoying because projects will take a while to wake up if no ones been there in a while and this can look less than great to recruiters etc. You know all this.

There are services that will ping your heroku projects every hour to keep them awake but they can feel sketchy and be impossible or difficult to turn off. Which is an issue if you're doing it too much and run out of dyno hours. Then all your projects shut down for the rest of the month.

You can write your own mini application to keep your projects awake without relinquishing precious control to other services though and learn a little bash and browser automation along the way.

These instructions are for bash but will be similar in powershell or zsh.

## TL;DR
  - Heroku servers go to sleep every hour
  - There are semi-sketchy services that keep them awake for you
  - You can write your own command line script to do this

## Setup:
  – These instructions are for bash but powershell / zsh should be similar
  - Make sure your Google Chrome is up-to-date

## Write the Code

### 1. Make a Bash File (.sh)

Make a new file anywhere you want on your computer called 'heroku.sh'. You can do this from the command line if you want.

'''bash
 $ touch heroku.sh
'''

Note that .sh indicates this is a bash script if you aren't using bash. 

### 2. Open the File

4. Open that file up so you can write in it. You can do this in an IDE like VSCode but you aren't going to be writing much code so maybe practice opening it in a command line text editor just for fun like 'nano', 'vim' or 'emacs'.

```bash
$ nano heroku.sh
```

sidenote: this actually makes a new file if it doesn't exist so you could just skip the previous step technically.

### 3. Write that Code

You can paste this code into your bash file but you might learn more by typing it out. 

Basically this is shell script (specifically bash syntax), meaning it could all be typed directly in your command line and would be valid syntax. We can put shell script into files though to save the trouble of typing things like this out repeatedly or to help if the commands form more complex multi-line scripts.

'''bash
while true
do
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --dump-dom https://YOURHEROKUSITE1.com
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --dump-dom https://YOURHEROKUSITE2.com
  sleep 1700
done
'''

Lets break that all down quickly.

'''bash
while true
do
  # ...
  sleep 1740
done
```

👆 This just sets up an infinite while loop with a 59 minute (1740 second) pause before repeating the loop.

```bash
  /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --headless --disable-gpu --dump-dom https://YOURHEROKUSITE1.com
```

👆 This uses your Chrome browser in headless mode (meaning no visual browser interface) and requests the DOM information. Thereby waking up the server.
