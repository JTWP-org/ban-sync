# ban-sync
ensure the correct players are banned everywhere

how it works ?

your going to need to make a repo with the blacklist.txt 

cd to where u want the file anywhere works 
(this is the url for ours but replace with yours )
`git clone https://github.com/JTWP-org/ban-sync.git`

remove the old blacklist.txt
 after you back it up ! 

`rm /home/steam/Pavlov/Saved/Config/blacklist.txt`

now you need to make a symbolic link from the blacklist.txt repo to the pavlovserver location 
here u will need to change the locations to match yours and if u have more than one server u can just link the repo blacklist to all the server locations 

`ln -s /home/steam/ban-sync/blacklist.txt /home/steam/pavlovserver/Pavlov/Saved/Config/blacklist.txt`

now we need to make a script to update it 

`nano /home/steam/ban-sync/update.sh`

inside this file add this 

-------------------------------------------------
`#!/bin/bash`

`git -C /home/steam/ban-sync/ pull`

------------------------------------------------

save and close 

then we need to give it perms to run 

`sudo chmod +x /home/steam/ban-sync/update.sh`

now to make the job and set how often to run it 

`sudo crontab -e -u root`

and add this line at the bottom 

`0 0 * * * bash /home/steam/ban-sync/update.sh`

this will run 1x a day at 12AM but u can edit the timer with the first chunk 0 0 * * *
this site can help u set it correctly 
https://crontab.guru/

close and save 
