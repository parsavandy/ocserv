# OpenConnect VPN Server Ubuntu
**2022 OCT UPDATE**: dockerized and added Dockerfile to run it anywhere you want on any Linux distro easily.
Buggy script for configuring OpenConnect (ocserv) protocol on the server easily and automatically.

**2023 JAN UPDATE**: added a help instruction for Docker custom installation so everyone can fully customized ocserv configuration for him/her self like port number, custom header, etc.

## Docker Installation
1. Install Docker
2. Build a docker image
```bash
docker build -t ocserv https://github.com/parsavandy/ocserv.git
```

3. Run the docker container
```bash
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -d ocserv
```

4. Add user
```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd testUserName
```

5. Change the user password
```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd testUserName
```

6. Delete user
```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -d testUserName
```

7. Lock the user
```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -l testUserName
```

8. Unlock user
```bash
docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -u testUserName
```

9. Show all users and their hashed password
```bash
docker exec -ti ocserv cat /etc/ocserv/ocpasswd
```

## Script Installation
Tested on Ubuntu 18.04 and 16.04.

Download and save the script on your server:
```bash
curl -O https://raw.githubusercontent.com/parsavandy/ocserv/main/ocserv-install.sh
```

Making script executable
```bash
chmod +x ocserv-install.sh
```

And then just run it:
```sh
./ocserv-install.sh
``` 
or
```sh
sudo bash ocserv-install.sh
``` 


## Features
- Easy install
- Easy uninstall
- Add User
- Change Password
- Show All Users
- Delete User
- Lock User
- Unlock User

## How to connect to it?
For making a connection to your server, you can use `AnyConnect`, `OpenConnect` or other alternative clients.

- AnyConnect: [GUI AnyConnect client for available platforms](https://it.umn.edu/vpn-downloads-guides).
- OpenConnect: [OpenConnect client for Linux](https://computingforgeeks.com/how-to-connect-to-vpn-server-with-openconnect-ssl-vpn-client-on-linux/).

And one more thing, contributions are welcome.

## How to customize the configuration?
In the docker way, at the beginning you have to clone the repo:
```sh
git clone https://github.com/parsavandy/ocserv.git
```

cd to the directory
```sh
cd ./ocserv
```
You can change the port, disable UDP, add a custom header, and so on.
Modify and customize ocserv.conf file and then build your image with modified ocserv.conf:
```sh
docker build . -t ocserv
```

Create a new container from ocserv image
```sh
docker run --name ocserv --privileged -p 443:443 -p 443:443/udp -d ocserv
```

The next steps like adding or removing users are the same as the Docker Installation part.

