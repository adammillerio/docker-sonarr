![https://linuxserver.io](https://www.linuxserver.io/wp-content/uploads/2015/06/linuxserver_medium.png)

The [LinuxServer.io](https://linuxserver.io) team brings you another quality container release featuring easy user mapping and community support. Be sure to checkout our [forums](https://forum.linuxserver.io) or for real-time support our [IRC](https://www.linuxserver.io/index.php/irc/) on freenode at `#linuxserver.io`.

# linuxserver/sonarr

![](https://sonarr.tv/img/logo.png)

[Sonarr](https://sonarr.tv/) (formerly NZBdrone) is a PVR for usenet and bittorrent users. It can monitor multiple RSS feeds for new episodes of your favorite shows and will grab, sort and rename them. It can also be configured to automatically upgrade the quality of files already downloaded when a better quality format becomes available.

## Usage

```
docker create \
	--name sonarr \
	-p 8989:8989 \
	-e PUID=<UID> -e PGID=<GID> \
	-v /dev/rtc:/dev/rtc:ro \
	-v </path/to/appdata>:/config \
	-v <path/to/tvseries>:/tv \
  -v <path/to/downloadclient-downloads>:/downloads \
	linuxserver/sonarr
```

**Parameters**

* `-p 8989` - the port sonarr webinterface
* `-v /dev/rtc:/dev/rtc:ro` - map hwclock to the docker hwclock as ReadOnly (mono throws exeptions otherwise)
* `-v /config` - database and sonarr configs
* `-v /tv` - location of TV library on disk
* `-e PGID` for for GroupID - see below for explanation
* `-e PUID` for for UserID - see below for explanation

### User / Group Identifiers

**TL;DR** - The `PGID` and `PUID` values set the user / group you'd like your container to 'run as' to the host OS. This can be a user you've created or even root (not recommended).

Part of what makes our containers work so well is by allowing you to specify your own `PUID` and `PGID`. This avoids nasty permissions errors with relation to data volumes (`-v` flags). When an application is installed on the host OS it is normally added to the common group called users, Docker apps due to the nature of the technology can't be added to this group. So we added this feature to let you easily choose when running your containers.  

## Info

* Monitor the logs of the container in realtime `docker logs -f sonarr`.

## Changelog

+ **20.07.16:** Rebase to xenial.
+ **31.08.15:** Cleanup, changed sources to fetch binarys from. also a new baseimage. 
