# Configuration

## Universal Control Plane (UCP)

The UCP is the centralized management tool for a Docker Enterprise Infrastructure. It is possible to run it into the Docker Community version of the Engine, but  with limited features.

To set up UCP we actually deploy it in Docker itself, which makes it pretty easy.

Command to install/run the UCP:
```
docker containter run --rm -it --name ucp -v /var/run/docker.sock:/var/run/docker.sock docker/ucp install --interactive
```

After that, it will ask you to create the admin user and password. Just for testing we don't need additional aliases.

After it completes it will show the URL to be able to reach the UCP.

![UCP Panel](../images/ucp-panel.png)

## Docker Swarm

Docker Swarm is a cluster management and orchestration feature that comes built into the Docker Engine. It creates `manager nodes` that are highly available and reliable to manage the `worker nodes` in case of failure