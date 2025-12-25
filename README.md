# Shinobi-EXP
I am running a my own _home server_ in __Lenovo ThinkCenter MiniPC__ with `Debian Linux` installed, and I wanted to include the home surveillance system into my server.
For this I used `shinobi` as surveillance system deployed as `container` with _Docker_.
This is the deployment I used to host `shinobi` surveillance system in my _server_.

### Starting Point

I wanted to deploy shinobi from one of official images and wanted to run __database__ as _separate_ container.
But official shinobi image comes with `MariaDB` integrated within and uses it as default, there are other third party solutions for the problem but I wanted to try for myself. So, made this.

## Details

### `docker-compose.yml`

* Used shinobi latest image from their official GitLab repository, and for reference used the pull date as the tag.
* Used the default config as base and modified according to my needs in the `config` directory.
* Used some files and configurations from older versions in `config/sql/` `config/init.sh`.
* Created `docker-compose.yml` to curate my needs for deploying the server as container,  
  
  - official `MariaDB` image for _database_ with custom authentication details.
  - mounted _Docker volume_ to store database files.
  - custom port exposing ability.
  - used `restart: always` for starting server on every boot.
  - mounted configurations at the their locations.
  - isolated network for this deployment.


### Connecting Cameras

* 2 VIGI network cameras powered by _POE switch_.  
* Made sure the cameras are on the same _network_ and _subnet_ as the PC.  
* Initialised cameras through their _web interface_.  
* Connection URL with their _IP address, ports, protocol_ and authentication details. [rtsp://user:pass@IP:port]  
* After logging in as `superuser` and creating users and permissions, added cameras as `moniters`.


### Accessing videos

* It is convenient to access videos and live feeds in _mobile phone_, so wanted a way to connect _mobile phone to the PC_.  
* The only way mobile connects to the network is through WiFi, so created _AccessPoint_ on the PC.  
* Installed services `hostapd` and `dnsmasq` to create _AccessPoint_. (Hotspot with DHCP server)  
* Anyone connected to the PC _AccessPoint_ can view cameras by specifying the shinobi port with the PC IP address on the WiFi.  
