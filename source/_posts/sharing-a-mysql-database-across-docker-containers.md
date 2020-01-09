title: Sharing a MySQL Database Across Docker Containers
date: 2020-01-09 18:23:47
tags:
- docker
- mysql
- containers
---

There are instances where you may have a database that is running on a host machine that you want to access from inside a container. There are three ways to do this depending on the situation.


### Using the Host Network

The [host networking](https://docs.docker.com/network/host/) mode will make the container use the same network as the host machine. This means the host machine and the container share the same IP and ports. So `localhost` inside the container is the same `localhost` in the host and you can connect to MySQL as if it was running in the same machine using `localhost`. 

```bash
docker run --network="host" <container>
```
This can be limiting in a lot of cases as you don't have the flexibility of an isolated container network with different ports and IP. 


### Using the Docker Bridge Network

Docker by default creates a network interface `docker0` on the host that all containers running on the host machine use. You can then use the IP address of host on the `docker0` (run `sudo ip addr show docker0` on the host) interface to connect from inside the container. The catch here is you will have to [enable remote access to MySQL](https://www.digitalocean.com/community/tutorials/how-to-allow-remote-access-to-mysql) by setting the `bind-address = 0.0.0.0`. This is usually a no-go for most situations.

### Sharing the MySQL Socket

Docker allows you to mount directories on your host machine to container. We can use this to share the socket used by MySQL. The socket is usually found at `/var/run/mysqld/mysqld.sock`. 

```bash
docker run -v /var/run/mysqld:/host/mysqld <container>
```

Now we can access the sock file inside the Docker container mounted at `/host/mysqld/mysqld.sock` and [connect to MySQL using the socket.](https://dev.mysql.com/doc/refman/5.5/en/connecting.html)

