seatsniper
=========

Requirements
--------
• Unix/Linux  
• *lynx* (May have to install, with [*homebrew*](http://brew.sh "homebrew site") it is: brew install lynx)  
• *Twilio* Account, sendmail, or other form of notification  

Setup
-------
###Main Program
You have to use fully qualified paths for the executables that are not 
included in you PATH variable. These aren't necessary if running manually from the root directory of the project, but the script isn't practical unless run from a cronjob, so absolute paths are a good idea when in doubt.
Open up tracker and change the lines marked #change (lines 6,7,8)

The first line sources the *alert.sh* script, importing those functions listed inside, in this case, it is the sendText function we are interested in. You have to make this alert.sh file, see alertExample.sh for a template. 

The second line is the folder where the program will keep site data, you should create this. 

The third line is the location of the lynx command. Find this with <code>which lynx</code> (This is necessary because cron jobs have a different PATH varibale from your bash shell, to set the cron path, see the *crontabExample.txt* file) Don't use relative paths here, becuase the directory that the cronjob runs from will not be the root directory of seatsniper.

###Twilio Notifications
Your program can send you text messages using the services of [*Twilio*](https://www.twilio.com "Twilio Home"), with a trial account, you can set it up so you can send messages to yourself for free. 



Usage
----
From root directory of seatsniper  
><code>$ ./tracker 'https://youwebsitehere'</code>  

The single quotes aren't necessary for all sites, but a required for some depending on the special characters in the URL

###Running from a crontab
To run the program in a crontab every minute     
<pre><code>$ cd ~
$ touch crontab.txt  
</code></pre>

Edit crontab.txt in any editor to include the line (see *crontabExample.txt* for more options)  
<code>0-59 * * * * /path/to/tracker http://yourwebsite.com</code>  
Save the text file and then back in terminal run   
<code>crontab ~/crontab.txt</code>  
You should receive some feedback that the cronjob has been installed and is running every minute


