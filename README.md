# Directions for running shiny apps in the browser with shiny-server

The Shiny Server installer will automatically install a systemd service called shiny-server, which will cause the shiny-server program to be started and stopped automatically when the machine boots up and shuts down. The shiny-server service will also be launched automatically when the installer has successfully installed the program.

To start or stop the server manually, you can use the following commands.

> sudo systemctl start shiny-server

> sudo systemctl stop shiny-server

You can restart the server with:

> sudo systemctl restart shiny-server

You can check the status of the shiny-server service using:

> sudo systemctl status shiny-server

And finally, you can use the enable/disable commands to control whether Shiny Server should be run automatically at boot time:

> sudo systemctl enable shiny-server

> sudo systemctl disable shiny-server

To start the server, run the following commands, respectively.

> sudo start shiny-server
# or 
> sudo shiny-server

To start the server, run the following commands, respectively.

> sudo stop shiny-server

# 2.7.3 Host Per-User Application Directories
# To ensure that the shiny-server publicly hosts any Shiny-apps in the user's ~/ShinyApps dir for users who are members of the "shinyUsers" group;
# run the following lines:

>  sudo groupadd shinyUsers
>  sudo usermod -a -G shinyUsers drew

# The Shiny-apps in the browser-enabled shiny-server are configured by the following file
> /etc/shiny-server/shiny-server.conf
# Here is an ecample config file

```run_as :HOME_USER:;

        # Define a server that listens on port 3838
	server {
		listen 3838;

	 location / {
		 user_dirs;
		 
		 # Define a location at the base URL

	 members_of shinyUsers;
    
		 #site_dir /srv/shiny-server;
		 #log_dir /var/log/shiny-server;

	  directory_index on;
    }
	  
# add user to the shinyUsers group so all shiny-apps in /home/$USER/ShinyApps/ will be available on this server at the URL http://server.com/$USER/ShinyApps. 
