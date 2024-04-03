# kondukto-secure-tunnel

Prerequisites
* Administrative privileges on the server.
* Docker installed on the server
* VPN configuration file, which will be provided privately.
* resolvconf should be installed

This document provides guidelines on how to set up a network configuration between the Kondukto client  and your network using WireGuard VPN(running on Docker container).

### 1. Enable IP Forwarding

Before making changes to the WireGuard configuration, ensure that IP forwarding is enabled on your server. You can do this by using the following commands:  
```
echo "net.ipv4.ip_forward = 1" | sudo tee -a /etc/sysctl.conf
echo "net.ipv4.conf.all.src_valid_mark=1" | sudo tee -a /etc/sysctl.conf
sudo sysctl -p
```

### 2. Run the Kondukto Client in a Docker Container

  
Use the following command to run the Kondukto client in a Docker container with WireGuard:

`sudo docker run -d --name=wireguard --network=host --restart=unless-stopped -v ~/wg_confs:/config -v /lib/modules:/lib/modules:ro -e PUID=1000 -e PGID=1000 --cap-add NET_ADMIN --cap-add SYS_MODULE linuxserver/wireguard`

This command runs the Kondukto client in a Docker container named 'wireguard'. The VPN configuration is placed under `~/wg_confs` in this example, but you can replace `~/wg_confs` with the path to your own VPN configuration directory.

  **Warning:** After running this Docker container, you might not be able to directly access the client machine on which the Docker is running due to the networking setup.
  
If everything is configured correctly, you should be able to establish a connection between kondukto client and your network



  

