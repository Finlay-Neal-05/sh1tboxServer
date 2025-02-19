

Most Important Notes:

- Don't do anything in the 'usage information' section until you have done its part in the installation section. The installation section is in order of the way I did it (top first).

- I installed crafty on the raid first, so its files for me are under /mnt/md0/Minecraft you should change this to the ssd you boot from, it will give you MUCH better performance. Call me about this if you want or you could try yourself.

- Commands are in [square brackets] and can be copy and pasted (don't copy the brackets, and you may need to change parameters like YOURPORT and USERNAME first) (right click to copy into powershell)

- I initially made the server using Ubuntu 20.04LTS, but I had to upgrade to 22.04LTS to install crafty, the minecraft server controller. It *should* be possible to install 22.04LTS or 24.04LTS first.

- First, watch a few of the videos in the quick links file, especially the first one because that is what I based everything off.

- When you set up the server, once you install and configure ssh you *shouldn't* have to use the gui on the server, it will work with only power and ethernet. 

- Speaking of, you shouldn't use wifi unless ABSOLUTELY NECESSARY. It will be super bad without ethernet.

- After installing and configuring you will be using windows powershell or termux for android to send commands to the server.

- Important to understand: Under [## Port forwarding SSH:] in the guide it tells you how to change the port that ssh uses, this makes port forwarding ssh safer but it means you have to add a tag in the ssh command in powershell or termux. For example before changing the port it would be [ssh USERNAME@YOURSERVERIP] and after changing the ssh port it would look like [ssh USERNAME@YOURSERVERIP -p YOURPORT] in the guide some things are referred to as the second one but you can just remove the -p and YOURPORT. This is key to understand but if you don't call me, it's hard to write in detail without making it complicated.

Important Notes:

- Change power and sleep setting to never turn off and change auto login to on. This will mean when you reboot it will auto login so you dont have to use GUI.

- You will need to change the IP on the server to reflect a LAN IP that isn't in use

- I have removed my name and put in USERNAME, you can set this to whatever you like just note that it should be all lowercase unless stated otherwise. And may have to follow other naming conditions like no spaces, etc.

- DO NOT PORT FORWARD SSH WITHOUT FOLLOWING THE STEPS IN THE GUIDE AND ONLY DO SO IF NECCESARY!

- I forgot to write down installing Plex but you shouldn't need to because you can just sign up for mine.

- You can download the .isos to create the bootable media from [https://releases.ubuntu.com/jammy/] for 22.04 and [https://releases.ubuntu.com/focal/] for 20.04

Maintenance:  

- If you end up using a raid you should check it by typing [cat /proc/mdstat] this will show the state of the raid (if any hard rives are dead) this is important and should be done often. (1-3 days) if possible

- You should also do [sudo apt update && sudo apt upgrade] often once every week or so or when you check the raid. 

- You can install 'termux' on your phone it's like powershell for android and it will make it faster.




