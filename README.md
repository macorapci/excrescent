# excrescent
This is a service that gives you fake websocket service.
I am using VPN which won't close the connection when ws connection is open on local. 
This is why I needed such a fake web socket so that the vpn connection would not close automatically.

## Create Websocket

### Download Websocat for Ubuntu

````console
sudo wget -qO /usr/local/bin/websocat https://github.com/vi/websocat/releases/latest/download/websocat.x86_64-unknown-linux-musl
sudo chmod a+x /usr/local/bin/websocat
websocat --version
````

### Create Bash File

````bash
#!/bin/bash

TIMEOUT_MIN=$(($1 * 60))
timeout --foreground $TIMEOUT_MIN websocat wss://ws.excrescent.com/web-socket
````

## Set Crontab

````
crontab -e
````

````console
*/10 * * * * ws-excrescent.sh 9
````

This crontab command mean is "Run in every 10 min" so we are giving timeout to '9'.