

###[Usage Information:]###




## General

- Password: [YOURPASSWORD] you don't have to put it here

- Location: [\\YOURSEVERIP\USERNAME-share]

- IP: [YOURSERVERIP]

- Login: [ssh USERNAME@YOURSERVERIP -p YOURPORT]

- Temporary External Login: [ssh USERNEAME@YOUPUBLICIP -p YOUPORT] this only works once ssh is port forwarded






## Raid

- Raid mount location: [/mnt/md0]

- Raid drive name: [md0]






## smb.conf:

- Access: [sudo nano /etc/samba/smb.conf]

- When making changes: [sudo service smbd restart]

- Added Text:
[USERNAME-share]
	comment = USERNAME Samba Share
	path = /mnt/md0/USERNAME-share
	read only = no
	browsable = yes






## Checking the HDDs

- First time only do [sudo apt install smartmontools]

- Then do [sudo smartctl --all /dev/sda] to check the drives. (Note: replace /dev/sda with the path of the drives. The Paths of the drives can be foud with [lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT] )






## Checking SSH Logs

- Type [sudo zgrep 'Ban' /var/log/fail2ban.log*] 

- Or type [sudo fail2ban-client status sshd]

- Or type [/etc/init.d/fail2ban status]






## Minecraft Server

- Crafty User: [] this is by default 'admin'

- Crafty Pass: [] this is randomly generated

- Get the public IP address: [curl https://ipinfo.io/ip] (You will need to install a package).

- Logging in to the server and running crafty:
	ssh in using [ssh USERNAME@YOURSERVERIP -p YOURPORT]
	Type [screen] and [enter] to be able to detach later.
	Then do [sudo su crafty -] to log in as the crafty user.
	Then do [cd /mnt/md0/minecraft/crafty && source .venv/bin/activate && cd /mnt/md0/minecraft/crafty/crafty-4 && python3 main.py] to quickly start crafty.
	Finally, Press [control + A + D] to detach from the screen.

- Alternatively logging in and starting crafty using individual commands:
	ssh in using [ssh USERNAME@YOURSERVERIP -p YOURPORT]
	Type [screen] and [enter] to be able to detach later.
	Then do [sudo su crafty -] to log in as the crafty user.
	Then do [cd /mnt/md0/minecraft/crafty] to change directory.
	Then do [source .venv/bin/activate] to run the virtual environment.
	Then do [cd /mnt/md0/minecraft/crafty/crafty-4] to change directory again.
	Then do [python3 main.py] to run crafty.
	Finally, Press [control + A + D] to detach from the screen.

- If you want to reattach later run [screen -r] a message may pop up saying there are multiple screens, e.g: [	3754.pts-0.USERNAME-server        (02/12/24 18:09:07)     (Detached) ] so type [screen -r 3754] in this case.

- To update crafty:
	first stop the instance (you can just [sudo reboot] )
	Then type [cd /mnt/md0/minecraft/crafty/crafty-4]
	Then [sudo su crafty]
	Then [git fetch && git pull] to get the update files
	Then [cd ..]
	Then [source .venv/bin/activate]
	Then [cd crafty-4]
	Then [pip3 install -r requirements.txt --no-cache-dir] To install the update.
	Then [exit] and start the server normally.

- Logging in is as simple as going to [https://YOURPUBLICIP:8443] Then Type in the user and pass. (the port by default is 8443 I think, you could change this and you should port forward this)

- Current Server Connection: [YOURPUBLICIP:port] where 'port' here is the individual port you select for each server.






## BeamMP Server

- Logging in to the server and running BeamMP:
	ssh in using [ssh USERNAME@YOURSERVERIP -p YOURPORT]
	Type [screen] and [enter] to be able to detach later.
	Then do [cd /home/USERNAME/BeamMP-Server/bin] to change directory.
	Then do [./BeamMP-Server] to run the server.
	Finally, Press [control + A + D] to detach from it.
	If you want to reattach later run [screen -r] a message may pop up saying there are multiple screens, e.g: [	3754.pts-0.USERNAME-server        (02/12/24 18:09:07)     (Detached) ] so type [screen -r 3754] in this case.

- You can do [nano /home/USERNAME/BeamMP-Server/bin/ServerConfig.toml] to change the config file press [ctrl + x] to exit [y] to save and [enter] to confirm

- Maps for the config file are as follows:
	/levels/gridmap_v2/info.json
	/levels/johnson_valley/info.json
	/levels/automation_test_track/info.json
	/levels/east_coast_usa/info.json
	/levels/hirochi_raceway/info.json
	/levels/italy/info.json
	/levels/jungle_rock_island/info.json
	/levels/industrial/info.json
	/levels/small_island/info.json
	/levels/smallgrid/info.json
	/levels/utah/info.json
	/levels/west_coast_usa/info.json
	/levels/driver_training/info.json
	/levels/derby/info.json






## Web Server (Apache2)

- Sensitive info was here ;)

- Copying files:
	From [cd /mnt/md0/USERNAME-share/...] you could change this to the location where you copy the website files from
	To [/var/www/NAMEHERE/html]

- Adding, removing and changing ports/file storage location: 
	[sudo nano /etc/apache2/ports.conf]
	[sudo nano /etc/apache2/sites-enabled/000-default.conf]
	[sudo service apache2 restart]






## Raid Failure 

- Make sure all partitions/drives detected [lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT]

- Then sudo [sudo mdadm --misc --examine /dev/XXX] replace [/dev/XXX] with drive path from previous command, e.g:
	sudo mdadm --misc --examine /dev/sda
	sudo mdadm --misc --examine /dev/sdb
	sudo mdadm --misc --examine /dev/sdc
	sudo mdadm --misc --examine /dev/sdd

- If a drive is simply out of sync, do the following commands, if a drive has failed, oh shit, hit the metaphorical panic button. [sudo umount -l /dev/md0] to unmount [/dev/md0]

- Then [sudo service smbd stop] to stop samba and allow stopping of mdadm.

- Then [sudo mdadm --stop /dev/md0] stop the array.

- Then [sudo mdadm --assemble /dev/md0] (won't assemble with all drives, don't sweat it).

- Then [sudo mdadm --manage /dev/md0 -a /dev/XXX] This is the main bit. You need to replace [/dev/XXX] with the name of the faulty drive you found with [lsblk]

- IMPORTANT: Make sure the drive is finished adding before you proceed, you can do [watch cat /proc/mdstat] to check it.

- Now you can start samba and mount the array again, [sudo service smbd start]

- And, [sudo mount /dev/md0]

- Useful commands:
	sudo blkid
	sudo mdadm --detail /dev/md0
	sudo mdadm --misc --examine /dev/XXX






###[Instructions:]###




- Disconnect all HDDs and USB drives (keyboard and mouse are fine)

- Boot up with the Ubuntu installer you chose to go with plugged in.

- When it does hardware checks you can insert the soon to be boot drive if its an external ssd or usb drive, ignore this if you have an m.2 or internal sata ssd.

- Follow prompts to install, Key settings:
	Keyboard: us
	Name: USERNAME (Capital first letter is OK here).
	Device name: USERNAME-server
	Username: USERNAME (all lowercase)
	Password not written here but you HAVE to remember it (duh).

- Once installed change wifi settings as such: Settings > Network > Wired connection > Settings gear > Ipv4. Key settings:
	Click 'manual' then change these settings
	Ip: 10.0.0.24
	Netmask: 255.255.255.0
	Gateway: 10.0.0.1
	Dns: 1.1.1.1

- Turn off the network connection and turn it back on again to save changes.

- Change power and sleep setting to never turn off.

- Open Terminal and type [sudo apt update && sudo apt upgrade] to update important software.

- Once finished type [sudo apt install openssh-server] it will do some stuff and then ask do you want to continue? type 'y' and press enter

- Type [sudo systemctl status ssh] to verify it's running

- Go to a windows PC and open powershell. Type [ssh USERNAME@YOURSERVERIP]

- It will say something like fingerprint cannot be secured do you want to connect still? type 'yes' and press enter.

- If the previous step did not work (You are at risk from a man in the middle attack or something like that) go to [c:/users/YOUR-USERNAME/.ssh/] then rename the file [known_hosts]. 
(If this doesn't work then you have done something wrong and you should change the name back).

- Done.






## Raid:

- Once logged in to the server using powershell use the command [sudo apt update && sudo apt upgrade] to make sure everything is up to date

- Use [sudo apt install mdadm] to install the raid software. (Press 'y' when prompted)

- Use the command [lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT] to see all drives and make note of the names. sda, sdb, etc.

- Use the command [sudo mdadm --create --verbose /dev/md0 --level=5 --raid-devices=4 /dev/sda /dev/sdc /dev/sdd /dev/sde] Notes:
	This is the command I used, you WILL need to change it to suite your needs.
	Sudo = run as admin
	mdadm = name of program
	--create = does what it says on the tin
	--verbose = prints info as it goes for debugging
	/dev/md0 = NOT THE NAME! This is the location/designation of the new raid drive. e.g c:/ on windows.
	--level=5 = Raid level
	--raid-devices=4 = The amount of raid devices to be used.
	/dev/sda... = The hard drives that will be used. (use the previous command to determine)

- SUPER IMPORTANT! DO NOT continue these instructions until the raid has been synced. (use command [watch cat /proc/mdstat] to see the current progress and to see when it finishes. This could take 10+ hours depending on the size of HDDs.

- Use the command [sudo mkfs.ext4 -F /dev/md0] to create an ext4 filesystem on the raid md0

- Create a mount point for the raid at /mnt/md0 [sudo mkdir -p /mnt/md0]

- Mount the raid at the mount point we created [sudo mount /dev/md0 /mnt/md0]

- Check that all those steps worked by running [df -h -x devtmpfs -x tmpfs]

- If everything looks good type [sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf] which will create a config file that will be loaded on startup.

- Do [sudo update-initramfs -u] to add the array to the RAM filesystem so it can be used at startup if anything important is on there.

- Do [echo '/dev/md0 /mnt/md0 ext4 defaults,nofail,discard 0 0' | sudo tee -a /etc/fstab] to automatically mount the raid at startup.

- Navigate to the raid drive by going [cd /mnt/md0] then use the command [sudo mkdir USERNAME-share] to make the folder samba will use. (You may need to do this via the gui on the server rather than the terminal).

- Done.

## Samba file share:






- Start by doing [sudo apt update && sudo apt upgrade] to make sure everything is up to date.

- Do [sudo apt install samba] to install samba.

- Do [samba --version] to make sure it's installed

- Do [sudo nano /etc/samba/smb.conf]. It will bring up a file, go to the bottom and add the following text:
	[USERNAME-share]
		comment = USERNAME Samba Share
		path = /mnt/md0/USERNAME-share
		read only = no
		browsable = yes

- Then press [ctrl + x] to exit [y] to save and [enter] to confirm.

- Then type [sudo service smbd restart] to restart and apply changes.

- Then type [sudo ufw allow samba] to allow the ubuntu firewall to allow samba traffic.

- Then type [sudo smbpasswd -a USERNAME] to create a password. (I just used the same password as the login)

- Type [sudo chmod --recursive ugo+rw /mnt/md0] to allow all users to access the files.

- Then type [sudo service smbd restart] again to apply changes.

- I kinda forgot to write how to connect to it in file explorer so text me and we can figure it out, or it might have been in the first video, IDK.






## Crafty Minecraft Server 

- First do [sudo apt update && sudo apt upgrade]

- Do [sudo apt install git python3 python3-dev python3-pip software-properties-common openjdk-8-jdk openjdk-8-jre] to install required packages. (You may need to install another package later).

- Do [sudo apt install screen] (Important later)

- Do [sudo useradd crafty -s /bin/bash] to create a crafty user.

- Do [sudo mkdir -p /mnt/md0/minecraft/crafty /mnt/md0/minecraft/server] to create the folders we will use.

- Do [sudo chmod --recursive ugo+rw /mnt/md0/minecraft] to take ownership of the files.

- Do [sudo chown -R crafty:crafty /mnt/md0/minecraft] to let the crafty user edit the files.

- IMPORTANT! Do [cd /mnt/md0/minecraft/crafty] to go to the directory we created.

- Do [git clone https://gitlab.com/crafty-controller/crafty-4.git] to get the crafty files and download them.

- Do [python3 -m venv .venv] To create a virtual environment to run the server in. (It may ask you to install another package. Do it.)

- Do [sudo su crafty -] to log in as the crafty user we created.

- IMPORTANT! As we are now logged in as the crafty user we can't/shouldn't use the command [sudo] before our commands as it can stuff up permissions.

- Do [source .venv/bin/activate] to activate the virtual environment.

- Do [cd /mnt/md0/minecraft/crafty/crafty-4] to go to a directory that was made when installing crafty. (Notice no [sudo]!)

- Do [pip3 install --no-cache-dir -r requirements.txt] If this doesn't work properly follow these steps.
	Type [exit]
	Run [sudo chmod --recursive ugo+rw /mnt/md0/minecraft] again
	Run [sudo chown -R crafty:crafty /mnt/md0/minecraft] again
	Do [sudo su crafty -] again
	Do [source .venv/bin/activate] again to enter the virtual environment.
	Do [cd /mnt/md0/minecraft/crafty/crafty-4] to change back to the directory.
	Do [pip3 install --no-cache-dir -r requirements.txt] Once more. (If it doesn't work: idk figure it out yourself. Haven't I helped you enough already??)

- Finally, do [python3 main.py] to run crafty. (See the top for logging in.)

- Done






## BeamMP Server:

- Do [sudo apt install liblua5.3-dev curl zip unzip tar cmake make git g++] to download dependencies

- From now on don't use sudo

- Do [git clone --recursive https://github.com/BeamMP/BeamMP-Server] to download the files from github.

- Type [cd BeamMP-Server] to change directory

- Do [git checkout tags/v3.4.1] IMPORTANT! Change 'v3.4.1' to the newest release of BeamMP

- Run [cmake -S . -B bin -DCMAKE_BUILD_TYPE=Release] To create some files idk.

- Run [cmake --build bin --parallel --config Release -t BeamMP-Server] to complete the installation. This may take some time.

- Next start the server to generate the files [cd /home/USERNAME/BeamMP-Server/bin] then [./BeamMP-Server]

- Then do [nano /home/USERNAME/BeamMP-Server/bin/ServerConfig.toml] press [ctrl + x] to exit [y] to save and [enter] to confirm once done.

- Add a server auth key in between the "". You can find them at: [https://keymaster.beammp.com/keys]

- Add other changes and save. Maps are as follows: 
	/levels/gridmap_v2/info.json
	/levels/johnson_valley/info.json
	/levels/automation_test_track/info.json
	/levels/east_coast_usa/info.json
	/levels/hirochi_raceway/info.json
	/levels/italy/info.json
	/levels/jungle_rock_island/info.json
	/levels/industrial/info.json
	/levels/small_island/info.json
	/levels/smallgrid/info.json
	/levels/utah/info.json
	/levels/west_coast_usa/info.json
	/levels/driver_training/info.json
	/levels/derby/info.json

- Start the server again. [cd /home/USERNAME/BeamMP-Server/bin] then [./BeamMP-Server]

- Done.






## Port forwarding SSH:

- Start by logging in and going [sudo nano /etc/ssh/sshd_config] 

- Uncommenting [#Port ...] and changing it to [Port YOURPORT] (or any other port)

- Save it by pressing [ctrl + x] to exit [y] to save and [enter] to confirm.

- Then type [sudo service sshd restart]

- From now on when connecting you must add a [-p 23105] to the end of the ssh command, e.g. [ssh wilkin@121.99.109.71 -p 23105]

- Next, disable root access, again do [sudo nano /etc/ssh/sshd_config] 

- Uncomment [#PermitRootLogin ...] and change it to [PermitRootLogin no]

- Save it by pressing [ctrl + x] to exit [y] to save and [enter] to confirm.

- Again type [sudo service sshd restart]

- Now, install fail2ban by typing [sudo apt install fail2ban]

- Check it is NOT running by typing [systemctl status fail2ban.service] do not run it because you have to change a few settings first.

- Type [cd /etc/fail2ban] this is fail2ban's directory

- Next, type [head -20 jail.conf] as you can see you should NOT change this document.

- Instead copy and rename it. [sudo cp jail.conf jail.local]

- Next type [sudo nano jail.local] to edit the new safe-to-edit document.

- Change the following settings: 
	ignoreip = 192.168.1.1 (Optional)
	bantime = 1440m (Change to whatever you want, in this case 24 hours)
	findtime = 20m (The time before, if you have made less than [maxretry] password guesses, your guesses will be reset). 
	maxretry = 5 (The amount of guesses you get)

- The Following setting is under [sshd]:
	port = YOURPORT

- Save it by pressing [ctrl + x] to exit [y] to save and [enter] to confirm.

- Next type [sudo systemctl enable fail2ban]

- Then, this is a one-off, type [sudo systemctl start fail2ban]

- To make sure it's all running type [sudo systemctl status fail2ban]

- To test it install an app called [termux] on your phone then turn on mobile data and login by typing [ssh USERNAME@YOURPUBLICIP -p YOURPORT] (you may need to type [pkg install openssh] first). 

- Once logged in, log out. Then try to log in again, but deliberately get the password wrong. Keep trying until it times out or says connection refused or connection timed out. 

- If you try more than 5 times more than [maxretry] times then you may want to log in again on the other computer or through LAN (ssh USERNAME@YOURSERVERIP -p YOURPORT)

- Type [sudo zgrep 'Ban' /var/log/fail2ban.log*] or alternatively [sudo fail2ban-client status sshd] or even [/etc/init.d/fail2ban status] for troubleshooting

- See if it shows that the ip was banned, if not, then see if there are any other errors and resolve them.






## Web Server (Apache2)

- Type [sudo apt update && sudo apt upgrade]

- Type [sudo apt install apache2 apache2-doc apache2-utils] to install apache2

- Type [sudo systemctl status apache2] to make sure it's running.

- Next, go to a web browser and type [YOURSERVERIP] or the local ip of the server, it should open a webpage.

- Next, you can replace the webpage with your own. Type Put your index.html and other files in a folder in the samba share. 

- Then, type [cd /mnt/md0/USERNAME-share/...] in powershell to go to the location stated above.

- Next, do [cp index.html style.css /var/www/html] to copy index.html and style.css to the location of the web server files.

- Refresh the website we used previously and it should bring up the new page. You can put in images too.

- To change the port, do [sudo nano /etc/apache2/ports.conf] to open the port configuration settings. Change the 80 in [Listen 80] to the port you wish to use for your webserver. You can also add multiple ports.

- Next, do [sudo nano /etc/apache2/sites-enabled/000-default.conf] change the port number in [<VirtualHost *:80>] to the port you used in the previous file. You can also change the location of the server files by changing [DocumentRoot /var/www/html].

- Next, save the file, and type [sudo service apache2 restart]. To access the web server now you must go to [YOURSERVERIP:port] change to the port you are using.






YOU'VE DONE EVERYTHING I'VE DONE CONGRATS!!

