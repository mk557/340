Min Kim 
IT 340 Project
Samba File Server 
 
Deliverables: 

- Install a Samba server on your computer || Configuring a few users that can connect to samba

Steps:
1. Installed Samba using the command apt-get install to obtain the Samba package. 	
2. Configured smb.conf file to enable setting for the Samba File Server for accessibility and security. Accessibility features such as setting the path for the folder I want to share and making that folder browsable. Security features such as allowing guests, specific users to be able to access the folder (in my case, smbgrp), and creating masks for the folder permission. Furthermore, server settings was set as localhost which was the default for demonstration purposes.
3. Created a samba directory called “share” in /srv/samba/share to allow users to share files through this folder.
4. Created users test1, test2, test3 to have a few users connect to the file server.
5. Created a new group called smbgrp and placed users test1, test2, and test3 in smbgrp to gain access privileges based on the group name.
6. Set the folder permissions as [nobody, smbgrp]. Nobody because I merely wanted to have an owner set for simplicity although it is a bad practice. However, the most important part about this was setting smbgrp as the group permission in order for that group to be able to read, write, and execute. 
7. Lastly, I ensured that the two critical services of Samba smbd and nmbd were up and running. Also, tested users to be able to access the file server and have access to read, write, and execute.

- Set a quota for the users
1. Installed quota using the command apt-get install to obtain the quota package.
2. Edited the file system table in /etc/fstab to enable usrquota or grpquota to the mounting options of my hard drive. However, I did setup my quota was usrquota, grpquota although grpquota wasn’t needed because I am setting up quotas for users.
3. Remounted the filesystem to make the changes and turned the quota on using quotaon /
4. Utilized the command edquota for users to set their soft and hard limits for disk quota sizes. 
5. Lastly, I checked if the configurations were successfully compiled by reporting quota and realized that changes were made correctly.

- Configure Nagios to monitor samba availability
1. Created a user called nagios and a group called nagcmd to run Nagios processes later and for other necessities. 
2. Installed the latest and most stable Nagios using the command apt-get install to obtain the Nagios package.
3. Extracted and compiled the package, configuring it with the group nagcmd.
4. Installed Apache2 and its utilities to obtain Nagios web interface. 
5. Installed necessary Nagios plugins, downloading it to my home directory, extracting the plugins, configuring the plugins as user nagios and group nagcmd to access and use the plugins. 
6. Installed the latest release of NRPE, extracted and also compiled the package with the group nagcmd.
7. To be able to utilize external commands through Nagios, I added the web server user, www-data to the nagcmd group. 
8. Additionally, xinetd was installed for the dependency of the service, NRPE. 
9. Configured Nagios by editing nagios.cfg to have a directory set to a path for the server I want to monitor. 
10. Created a new directory that the path was set to because it will store configuration files for my server.
11. Configured commands.cfg to add a new command called check_nrpe that will allow the use of nrpe commands for nagios to monitor my server.
12. Added my host configuration by creating a new config file called sambaserver.cfg in the path that I set my configurations to be for the server.
13. Defined necessary services for Nagios to monitor samba availability such as smbd and nmbd that are required for the samba server.
14. Lastly, I ensured that the two services nagios and apache2 were up and running, along with NRPE and xinetd service that are correlated to monitor the server successfully.

- Configure Nagios to monitor samba user disk utilization
1. To monitor samba user disk utilization, I used the plugin called check_disk_smb and defined it in the commands.cfg file with the necessary arguments that were needed to be made.
2. I configured it to match my WORKGROUP, share folder, and user information to gain information about my share folder. 
3. I set up an argument to provide a warning and critical sign on Nagios to monitor the disk usage of the file server.

- Monitor CPU Usage, Memory Usage
1. Obtained two Nagios plugins called check_cpu and check_memory from the web and extracted it into my directory.
2. Copied the plugins to my libexec directory of my Nagios server and set the file permissions as needed. 
3. Changed the owner and group of the plugins to user nagios and group nagios to utilize the plugins.
4. Utilizing the ./ -h command to check_cpu and check_memory arguments, I was able to set commands for the two plugins in the commands.cfg.
5. Implemented the plugins to my localhost server config and allow Nagios to monitor these services.
