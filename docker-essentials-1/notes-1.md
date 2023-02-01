# Introduction and Installation Prep

The course tells us to install an Ubuntu server VM, but if we use linux we can just install Docker directly (my case). In the course, they don't mention the ["Docker Desktop" edition for Linux](https://docs.docker.com/desktop/install/linux-install/), only for Windows and Mac, probably because by that time it was still not launched for linux. But now we already have that for Linux and that is recommended instead of the Docker Engine CE edition. Check the differences between the editions in this [link](https://docs.docker.com/desktop/faqs/linuxfaqs/#what-is-the-difference-between-docker-desktop-for-linux-and-docker-engine). But to follow along with the course, I created the Ubuntu VM and installed the [Docker Engine](https://docs.docker.com/engine/install/)

## Steps to Install Docker Engine

1. Make sure any old version of docker is uninstalled
```
sudo apt-get remove docker docker-engine docker-ce docker.io
```

2. Update packages
```
sudo apt-get update
```

3. Allow Apt to use a repository over HTTPS
```
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```

4. Add the Docker Official GPG Key to Apt
```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

5. Verify that you have the Docker GPG key
```
sudo apt-key fingerprint 0EBFCD88
```

6. Add the Docker Repository to Apt
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

7. Update packages AGAIN
```
sudo apt-get update
```

8. Install Docker
```
sudo apt -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

9. Post Installation scripts
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

10. Logout and Log back in to apply the group and user changes

11. Test if docker was installed successfully
```
docker run hello-world
```

## Troubleshooting issues

### Could not connect to the docker daemon

If you get an error saying that it could not connect to the docker daemon, make sure that it is running. This, along with the user not having been added to the docker group, is the most common issue that usually happens.

Error message:
*"Can't connect to docker daemon. Is 'docker -d' running on this host?"*

A good fix is to enable the docker daemon to always start on boot with systemd.

```
sudo systemctl enable docker
```

Or you could just start the docker service manually, but you would need to always do it to use Docker the first time you log into the machine:
```
sudo systemctl start docker
```
Or:
```
sudo service docker start
```

### Other issues

For other issues you are trying to troubleshoot, I suggest you take a look at the Docker documentation, they have a specific section for [Troubleshoot and diagnose](https://docs.docker.com/desktop/troubleshoot/overview/)