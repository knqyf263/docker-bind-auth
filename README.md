# docker-bind-auth
BIND9 auth server on Docker

#Introduction
Dockerfile to create a Docker container image for BIND DNS server(authoritative name server).

BIND is open source software that implements the Domain Name System (DNS) protocols for the Internet. It is a reference implementation of those protocols, but it is also production-grade software, suitable for use in high-volume and high-reliability applications.

## Contributing

If you find this image useful here's how you can help:

- Send a pull request with your awesome features and bug fixes
- Help users resolve their [issues](../../issues?q=is%3Aopen+is%3Aissue).

## Issues
Before reporting your issue please try updating Docker to the latest version and check if it resolves the issue. Refer to the Docker [installation guide](https://docs.docker.com/installation) for instructions.

SELinux users should try disabling SELinux using the command `setenforce 0` to see if it resolves the issue.

If the above recommendations do not help then [report your issue](../../issues/new) along with the following information:

- Output of the `docker version` and `docker info` commands
- The `docker run` command or `docker-compose.yml` used to start the image. Mask out the sensitive bits.
- Please state if you are using [Boot2Docker](http://www.boot2docker.io), [VirtualBox](https://www.virtualbox.org), etc.

# Getting started

## Installation

This image is available as a [trusted build](//hub.docker.com/r/sameersbn/bind) on the [Docker hub](//hub.docker.com) and is the recommended method of installation.

```bash
$ docker pull knqyf263/bind-auth:latest
```

Alternatively you can build the image yourself.

```bash
$ git clone https://github.com/knqyf263/docker-bind-auth.git
$ cd docker-bind-auth
$ docker build --tag $USER/bind .
```

## Quickstart

Start BIND using:

```bash
$ docker run --name bind -d --publish 53:53/udp knqyf263/bind-auth:latest
```

```bash
$ dig @127.0.0.1 www.example.com

; <<>> DiG 9.8.3-P1 <<>> @127.0.0.1 www.example.com
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 4916
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 2, AUTHORITY: 2, ADDITIONAL: 2

;; QUESTION SECTION:
;www.example.com.               IN      A

;; ANSWER SECTION:
www.example.com.        3600    IN      CNAME   host1.example.com.
host1.example.com.      3600    IN      A       192.168.1.5

;; AUTHORITY SECTION:
example.com.            3600    IN      NS      ns2.example.com.
example.com.            3600    IN      NS      ns1.example.com.

;; ADDITIONAL SECTION:
ns1.example.com.        3600    IN      A       192.168.1.2
ns2.example.com.        3600    IN      A       192.168.1.3

;; Query time: 0 msec
;; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Mon Sep  7 19:11:50 2015
;; MSG SIZE  rcvd: 137
```


# Maintenance

## Upgrading

To upgrade to newer releases:

  1. Download the updated Docker image:

  ```bash
  $ docker pull knqyf263/bind-auth:latest
  ```

  2. Stop the currently running image:

  ```bash
  $ docker stop bind
  ```

  3. Remove the stopped container

  ```bash
  $ docker rm -v bind
  ```

  4. Start the updated image

  ```bash
  $ docker run -name bind -d [OPTIONS] knqyf263/bind-auth:latest
  ```

## Shell Access

For debugging and maintenance purposes you may want access the containers shell. If you are using Docker version `1.3.0` or higher you can access a running containers shell by starting `bash` using `docker exec`:

```bash
$ docker exec -it bind bash
```
