# Getting Started with Project Nautilus

[![asciicast](https://asciinema.org/a/7mT0ZiVOBtJawDHg3zERfjkxA.svg)](https://asciinema.org/a/7mT0ZiVOBtJawDHg3zERfjkxA)

Project Nautilus is included with the VMware Fusion Tech Preview 20H1 release. No additional software is necessary.

### Install Fusion Tech Preview 20H1 build
Fusion Tech Preview 20H1 can be installed on the same host as the current shipping VMware Fusion "GA" version (currently 11.5.1). Note that only one copy of Fusion or Fusion Tech Preview can be running at a given time. To use 'vctl' and Project Nautilus, make sure that Fusion 11.5.1 is not running.

### Prepare your system

In order to properly run containers on the Mac using Fusion, we need to make some inital adjustments to the system. 
These changes include:
- Creating a case-sensitive volume for storing container images 
- - you can see this mounted on your desktop once the services start
- Creating a container network using vmnet
- launching the container runtime system service

Nautilus has a single command to both prepare the system and initiate the services:

```
% vctl system start

vctl system start
Preparing storage...
Container storage has been prepared successfully under /Users/mike/.nautilus/storage
Preparing container network, you may be prompted to input password for administrative operations...
Password:
Container network has been prepared successfully using vmnet:  vmnet12
Launching container runtime...
Container runtime has been started.

```

If you prefer you can also customize the preperation. This will allow you to set new defaults for the PodVM size, as well as the size of the container storage volume.

```
% vctl system prepare [options]

OPTIONS:
  -c, --cache-location string   Specify a location to store cache file (default "/Users/mike/.nautilus")
  -s, --dmg-size string         dmg file size (default "128g")
  -h, --help                    help for prepare
  -m, --mount-name string       Mount name for container storage (default "nautilus")
  -u, --vm-cpu int              CPU cores of base virtual machine (default 2)
  -o, --vm-mem int              Memory size (MB) of base virtual machine (default 1024)

```

### Pull an image from a remote repository
To run a container, you will firstly need to get an image from a repository. The image can be from dockerhub, or a private image registry such as Harbor.

```
% vctl pull image docker.io/library/nginx:latest

───                                                                                ──────   ────────
REF                                                                                STATUS   PROGRESS
───                                                                                ──────   ────────
index-sha256:8aa7f6a9585d908a63e5e418dc5d14ae7467d2e36e1ab4f0d8f9d059a3d071ce      Done     100% (1412/1412)
manifest-sha256:89a42c3ba15f09a3fbe39856bddacdf9e94cd03df7403cad4fc105088e268fc9   Done     100% (948/948)
layer-sha256:b65031b6a2a591fa0fcb63064aa17177636915499deab5cfc54eb71e63df8036      Done     100% (203/203)
layer-sha256:8ec398bc03560e0fa56440e96da307cdf0b1ad153f459b52bca53ae7ddb8236d      Done     100% (27092274/27092274)
config-sha256:c7460dfcab502275e9c842588df406444069c00a48d9a995619c243079a4c2f7     Done     100% (6670/6670)
layer-sha256:dfb2a46f8c2c9c83e5aad082a5f8c3f366fd5a56fa322ed0c84a4c3436864d17      Done     100% (23741331/23741331)
INFO Unpacking docker.io/library/nginx:latest...
INFO done
```


### Run the container image
Once the image has been pulled locally, you can run it as a new container. Here we're also specifying the '-d' flag which detatches the host console session from the running container. 

```
% vctl run container myNginx1 -d -i  docker.io/library/nginx:latest

INFO container myNginx1 started and detached from current session
```

### Verify the container is running

You can now see the container status as 'running' with "vctl get container", or use a built-in alias:

```
% vctl ls c

────       ─────                                ───────                ──               ─────   ──────    ─────────────
NAME       IMAGE                                COMMAND                IP               PORTS   STATUS    CREATION TIME
────       ─────                                ───────                ──               ─────   ──────    ─────────────
myNginx1   docker.io/library/nginx:latest       nginx -g daemon off;   172.16.223.129           running   2020-01-20T17:48:52-08:00
```


Now you can launch a web browser to navigate to the IP of the nginx container which is now up and running.


## Stop/Start the container
You can stop the container to free up resources with following command:

```
% vctl stop container mynginx1
INFO container myNginx1 has been stopped
```

You can start a stopped container with start command:

```
% vctl start container myNginx1 -d
INFO container myNginx1 started and detached from current session
```

### Get or List images

vctl provides a convenient way to show the images and running contianers. Use 'get' or 'list' or 'ls' to show some basic information about an object type.

```
% vctl get image
```
OR using aliases

```
% vctl ls i
────                                 ─────────────               ────
NAME                                 CREATION TIME               SIZE
────                                 ─────────────               ────
docker.io/library/nginx:latest       2020-01-20T17:42:50-08:00   48.5 MiB
docker.io/mikeroysoft/mrs-hugo:dev   2020-01-19T17:46:09-08:00   25.0 MiB
```



### Get containers
Similar to Images, you can use "vctl get containers" to get a list of running containers. To get a full list of containers, including those are not running, you can use command below:

```
% vctl get containers -a
────       ─────                                ───────                ──               ─────   ──────    ─────────────
NAME       IMAGE                                COMMAND                IP               PORTS   STATUS    CREATION TIME
────       ─────                                ───────                ──               ─────   ──────    ─────────────
my-www     docker.io/mikeroysoft/mrs-hugo:dev   nginx -g daemon off;   172.16.223.128           running   2020-01-19T17:58:33-08:00
myNginx1   docker.io/library/nginx:latest       nginx -g daemon off;   172.16.223.129           running   2020-01-20T17:48:52-08:00
```


### CLI available with this tech preview
You can type "vctl" to get a list of commands available to run containers.  



### Advanced Use Cases
More detailed information of container

You can use "vctl describe" to get detailed information of a container, the virtual machine that hosts this container, rootfs of the container. 

```
% vctl describe container mynginx1
vctl describe container myNginx1
Name:                       myNginx1
Status:                     running
Command:                    nginx -g daemon off;
Container rootfs in host:   /Users/mike/.nautilus/storage/containerd/root/io.containerd.snapshotter.v1.native/snapshots/9
IP address:                 172.16.223.129
Creation time:              2020-01-20T17:48:52-08:00
Image name:                 docker.io/library/nginx:latest
Image size:                 48.5 MiB
Host virtual machine:       /Users/mike/.nautilus/.r/vms/myNginx1/myNginx1.vmx
Container rootfs in VM:     /.containers/myNginx1
Access in host VM:          vctl sh vm -c myNginx1
Exec in host VM:            vctl exec vm /Users/mike/.nautilus/.r/vms/myNginx1/myNginx1.vmx -- /bin/ls

```



### Shell access into the container VM

Nautilus has the ability to shell into the container host, or PodVM, of the specified container.

Example:

```
% vctl sh vm -c myNginx1
sh-4.4#
```

### Keep the VM running after container stopped

By adding the "-k" parameter when running a container, when the container exits its PodVM will keep running. You can still 'vctl sh vm' into the container host to inspect logs and debug info.

### Known Limitations and issues

See this document: [Known Limitations](./known-limitations.md)

