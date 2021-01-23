Originally forked from https://github.com/daevien/phantombot-docker so it can run on ARM processors.

First time run as interactive if you have no existing config:

```
docker run -it --name phantombot -v /PATH/TO/CONFIG:/phantombot/config -v /PATH/TO/BACKUP:/backup -v /etc/localtime:/etc/localtime:ro -p 25000:25000 axiol/phantombot:latest
```

Example docker-compose.yml once a config is supplied:

```
version: "3.7"

services:
    phantombot:
      container_name: phantombot
      volumes:
        - '/PATH/TO/CONFIG:/phantombot/config'
	- '/PATH/TO/BACKUP:/backup'
        - '/etc/localtime:/etc/localtime:ro'
      environment:
        - APIOAUTH=data_goes_here
        - BASEPORT=25000
        - CHANNEL=owner
        - OWNER=owner        
	- MSGLIMIT30=19.0
        - MUSICENABLE=true
        - OAUTH=data_goes_here
        - PANELPASSWORD=password
        - PANELUSER=username
        - USEHTTPS=false
        - USER=botname
        - WEBAUTH=data_goes_here
        - WEBAUTHRO=data_goes_here
        - WEBENABLE=true
        - WHISPERLIMIT60=60.0
        - YTAUTH=data_goes_here
        - YTAUTHRO=data_goes_here
      ports:
        - 25000:25000
        - 25003:25003
        - 25004:25004  
      image: 'axiol/phantombot'
```      
      
Old info follows, this is not current. Will work on updating it.

# What is this?
* Docker container
* Phantombot
* Alpine Linux 
* Settings are saved upon restart
* Automatic backup every 24 hours (defaults at 2:37 AM)
* Includes both stable & nightly builds 
* Nightly images are renewed every 24h 

# Functionality
* 100%

--> Please let me know if anything fails to work!

# How to run
* Decide which branch to use. Currently there are three branches available: nightly (for the nightly development builds), stable (for the latest stable version, currently 3.0.0), and 2.4.2 (the latest stable version of the 2.x series). Please never use the 'latest' version, as you might get a different version from what you're expecting!
* You will need to mount the config files so your settings and data will be saved upon exit.
* The keystore.jks file is optional (only add it when using https).
* Edit the command below according to your needs.
* Finally open ports 25000-25004 of your firewall.
```sh
docker run -it \ 
	--name phantombot \
	-v /PATH/TO/CONFIG:/phantombot/config \
	-v /PATH/TO/BACKUP/:/backup \
	-v /etc/localtime:/etc/localtime:ro \
	-p 25000:25000 \
	axiol/phantombot
```
(Personally, I use /DOCKER_ROOT/phantombot as the /PATH/TO/BOT, the original source of this docker uses specific mapping to files but I've changed it to map the whole directory as I'm intending to add in some customization.

# All botlogin.txt arguments
Below are all the args for use on twitch with any of the following optionally enabled: HTTPS, Mariadb/MySQL, Streamlabs, Gamewisp, Discord, Twitter and Youtube.

For more information on the arguments below, please click [here](https://community.phantombot.tv/t/settings-for-botlogin-txt/78) .
Booleans are set with *true* or *false*.

### BASIC CONFIGURATION
* baseport=*Starting port, normally 25000*
* owner=*Name of the broadcaster*
* clientid=*Typically blank or not set. Can be obtained from Twitch*
* devcommands=*To help live debug with users. Enabled by default*
* logtimezone=*Specifies a timezone for logging*
* msglimit30=*No. of messages allowed to send to Twitch within 30 secs*
* musicenable=*Boolean, to enable/disable the Youtube player web interface*
* panelpassword=*Password to access the control panel and Youtube player*
* paneluser=*User used to access the control panel and Youtube player*
* twitch_tcp_nodelay=*Boolean, enabling sends  messages faster vs costing bandwith. Default=enabled*
* usemessagequeue=*Boolean, disabling removes delay between messages. Default=enabled*
* user=*Name of your Phantombot*
* web_enable=*Boolean, enable/disable the web server*
* whisperlimit60=*Number of whispers allowed in 60 seconds. Not used at present*
### HTTPS---how-to [here](https://community.phantombot.tv/t/how-to-enable-ssl-on-phantombot/71)
* usehttps=*Boolean, requires httpsFilename and httpsPassword to be set*
* httpsFileName=*/PATH/TO/keystore.jks*
* httpsPassword=*Password of keystore.jks*
### MARIADB/MYSQL/SQLITE/INISTORE
* datastore=*mysqlstore/inistore (text-based on-disk system). Default=SqlLite3*
* datastoreconfig=*/PATH/TO/FILE for inistore and SQLite3. Configures different data store types* 
### FOR MARIADB/MYSQL---how-to [here](https://community.phantombot.tv/t/mysql-configuration/73)
* mysqlhost=*Hostname of host*
* mysqlname=*Name of database*
* mysqlpass=*Password of user*
* mysqlport=*Set if Mariadb/MySQL runs on alternative port*
* mysqluser=*Name of user*
### TWITCH CREDENTIALS
* oauth=*Twitch IRC chat OAuth token. Get it [here](https://twitchapps.com/tmi/) *
* apioauth=*API OAuth key. Get it [here](https://twitchapps.com/tokengen/) *
* channel=*Twitch channel phantombot will log into*
### TWITTER CREDENTIALS---how-to [here](https://community.phantombot.tv/t/twitter-integration-setup/65)
* twitterUser=*Name of Twitter account*
* twitter_consumer_key=*Twitter authorization key*
* twitter_consumer_secret=*Twitter authorization key*
* twitter_access_token=*Twitter authorization key*
* twitter_secret_token=*Twitter authorization key*
### STREAMLABS CREDENTIALS---how-to [here](https://phantombot.tv/streamlabs/)
* twitchalertskey=*Streamlabs (previously TwitchAlerts) authentication key*
* twitchalertslimit=*Max no of donations to query in 1 go. Keep low*
### DISCORD_CREDENTIALS---how-to [here](https://community.phantombot.tv/t/discord-integration-setup/64)
* discord_token= *Discord token*
### GAMEWISP CREDENTIALS---how-to [here](https://phantombot.tv/gamewisp/)
* gamewispauth=*Autorization token*
* gamewisprefresh=*Autorization refresh token*
### YOUTUBE CREDENTIALS
* youtubekey=*Optional. Phantombot provides one internally*
