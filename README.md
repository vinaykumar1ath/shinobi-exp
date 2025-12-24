# Shinobi-EXP

This is the deployment I used to host shinobi surveillance system in my Debian system.

### Starting Point

I wanted to deploy shinobi from one of official images and wanted to run database separate from the main container.
But official shinobi image comes with MariaDB integrated within and uses it as default, there are other third party solutions for the problem but I wanted to try for myself. So, made this.

## Details

### `docker-compose.yml`

* Used shinobi latest image from their official GitLab repository, and for reference used the pull date as the tag.
* Used the default config as base and modified according to my needs in the `config` directory.
* Used some files and configurations from older versions in `config/sql/` `config/init.sh`.
* Created `docker-compose.yml` to curate my needs for deploying the server as container,

    * official MariaDB image for database with custom authentication details.
    * mounted volume to store database files.
    * custom port exposing ability.
    * used `restart: always` for starting server on every boot.
    * mounted configurations at the their locations.
    * isolated network for this deployment.


### Connecting Cameras

* 2 VIGI network cameras powered by POE switch.
* Made sure the cameras are on the same network and subnet as the PC.
* Initialised cameras through their web interface.
* Connection URL with their IP address, ports, protocol and authentication details. [rtsp://user:pass@IP:port]
* After logging in as `superuser` and creating users and permissions, added cameras as `moniters`.


### Accessing videos

* It is convenient to access videos and live feeds in my phone, so wanted a way to connect my phone to the PC.
* The only way mobile connects to the network is through WiFi, so created `AccessPoint` on the PC
* Installed services `hostapd` and `dnsmasq` to create `AccessPoint`. (Hotspot with DHCP server)
* Anyone connected to the PC `AccessPoint` can view cameras by specifying the shinobi port with the PC IP address on the WiFi.
