# Getting Started with Project Nautilus

Project Nautilus is included with VMware Fusion 11.5.5 and the Fusion Tech Preview 20H2 releases. No additional software is necessary.

### Install Fusion Tech 11.5.5 or Tech Preview 20H2
Fusion 11.5.5 now includes vctl! Update from any prior version and it becomes instantly available at the command line. 

vctl is also updated in the latest Tech Preview 20H2, and can be installed on the same host as the current shipping VMware Fusion "GA" version. Note that only one copy of Fusion or Fusion Tech Preview can be running at a given time.

### Start the vctl service

The first operation is to start the container runtime. On first launch, `vctl system start` automatically prepares the system with the dependenceis it needs, including:

- Creating a case-sensitive volume for storing container images 
  - you can see this mounted on your desktop once the services start
- Creating a container network using vmnet
- launching the container runtime system service


```
> vctl system start

Preparing storage...
Container storage has been prepared successfully under /Users/mike/.vctl/storage
Preparing container network, you may be prompted to input password for administrative operations...
Password:
Container network has been prepared successfully using vmnet: vmnet16
Launching container runtime...
Container runtime has been started.

```


If you prefer you can also customize the preparation. This will allow you to set new defaults for the contaeinr appliance vm size, as well as the size of the container storage volume.

You can also specify these parametes when executing `vctl run` by using the **-c** and **-m** flags.


```
USAGE:
  vctl system config [OPTIONS]

OPTIONS:
      --cache-location string   Specify the cache file location (default "/Users/mike/.vctl")
  -h, --help                    Help for config
      --mount-name string       Mount name for container storage (default "Fusion Container Storage")
  -s, --storage string          Container storage size (default "128g")
  -c, --vm-cpus int             CPU cores of base virtual machine that hosts container (default 2)
  -m, --vm-mem int              Memory size (MB) for virtual machine that hosts container (default 1024)

EXAMPLES:
  # To configure the virtual machine that hosts container with 4 CPU cores and 2GB memory by default.
  vctl system config --vm-cpus 4 --vm-mem 2048

```

### Pull an image from a remote repository
To run a container, you will firstly need to get an image from a repository, or you'll need to build one from a Dockerfile. Images are by default pulled from dockerhub, but a private image registry such as Harbor can be used as well.

```
> vctl pull nginx
INFO Pulling from index.docker.io/library/nginx:latest
───                                                                                ──────   ────────
REF                                                                                STATUS   PROGRESS
───                                                                                ──────   ────────
index-sha256:30dfa439718a17baafefadf16c5e7c9d0a1cde97b4fd84f63b69e13513be7097      Done     100% (1412/1412)
manifest-sha256:8269a7352a7dad1f8b3dc83284f195bac72027dd50279422d363d49311ab7d9b   Done     100% (948/948)
layer-sha256:11fa52a0fdc084d7fc3bbcb774389fd37b148ee98e7829cea4af189735acf848      Done     100% (203/203)
layer-sha256:afb6ec6fdc1c3ba04f7a56db32c5ff5ff38962dc4cd0ffdef5beaa0ce2eb77e2      Done     100% (27098756/27098756)
config-sha256:9beeba249f3ee158d3e495a6ac25c5667ae2de8a43ac2a8bfd2bf687a58c06c9     Done     100% (6670/6670)
layer-sha256:b90c53a0b69244e37b3f8672579fc3dec13293eeb574fa0fdddf02da1e192fd6      Done     100% (23922586/23922586)
INFO Unpacking nginx:latest...
INFO done
```

### Build a new container image

You can use a standard dockerfile to build a new container image, rather than downloading a pre-packaged one.  vctl also supports multi-stage builds. The process to simply `cd` into a directory with a `Dockerfile` and executing `vctl build .`

```
> vctl build -t myImage:latest .
vctl build -t myImage:latest .
INFO building image myImage:latest with jobId 92f6eea9-2892-4400-ba5c-b83412f5100c using internal builder instance...
INFO preparing base images...

... (full stack omitted for brevity)

INFO[0018] Taking snapshot of files...
INFO[0018] Generating final image file...
INFO[0019] Finished generating final image file
INFO creating image myImage:latest
INFO successfully built image myImage:latest

```

### Run the container image
Once the image has been built or pulled locally, you can run it as a new container. Here we're also specifying the '-d' flag which detaches the host console session from the running container. 

```
> vctl run -n myNginx -t -d nginx
INFO container myNginx started and detached from current session

```

### Verify the container is running

You can now see the container status as 'running' with `vctl ps`:

```
> vctl ps
────      ─────          ───────                ──                ─────   ──────    ─────────────
NAME      IMAGE          COMMAND                IP                PORTS   STATUS    CREATION TIME
────      ─────          ───────                ──                ─────   ──────    ─────────────
myNginx   nginx:latest   nginx -g daemon off;   192.168.243.128   n/a     running   2020-05-28T15:29:51-07:00
```
 
To get a full list of containers, including those are not running, you can add the **-a** flag:


```
> vctl ps -a
────      ─────            ───────                ──                ─────   ──────    ─────────────
NAME      IMAGE            COMMAND                IP                PORTS   STATUS    CREATION TIME
────      ─────            ───────                ──                ─────   ──────    ─────────────
myImage   myImage:latest   nginx -g daemon off;   n/a               n/a     stopped   2020-05-28T16:10:27-07:00
myNginx   nginx:latest     nginx -g daemon off;   192.168.243.128   n/a     running   2020-05-28T15:29:51-07:00
```

Now you can launch a web browser to navigate to the IP of the nginx container appliance (192.168.243.128 in the case of the example above) which is now up and running.  No need to map ports unless you want to.


### Stop/Start the container
You can stop the container to free up resources with following command:

```
> vctl stop myNginx
INFO container myNginx has been stopped
```

You can re-start a stopped container with start command:

```
> vctl start myNginx -d
INFO container myNginx started and detached from current session
```

### List images

vctl provides a familiar way to show images and containers. Use `vctl images` to show info about the local stored images

```
> vctl images
────           ─────────────               ────
NAME           CREATION TIME               SIZE
────           ─────────────               ────
nginx:latest   2020-05-28T15:29:26-07:00   48.7 MiB
```



### vctl commands
You can type `vctl` with no arguments to get a list of commands available to run containers.  

```
USAGE:
  vctl COMMAND [OPTIONS]

COMMANDS:
  build       Build a container image from a Dockerfile.
  create      Create a new container from a container image.
  describe    Show details of a container.
  exec        Execute a command within a running container.
  execvm      Execute a command within a running virtual machine that hosts container.
  help        Help about any command.
  images      List container images.
  ps          List containers.
  pull        Pull a container image from a registry.
  push        Push a container image to a registry.
  rm          Remove one or more containers.
  rmi         Remove one or more container images.
  run         Run a new container from a container image.
  start       Start an existing container.
  stop        Stop a container.
  system      Manage the Nautilus Container Engine.
  tag         Tag container images.
  version     Print the version of vctl.

Run 'vctl COMMAND --help' for more information on a command.
```



### Advanced Use Cases

You can use `vctl describe` to get more detailed information of a container, the virtual machine that hosts this container, rootfs of the container and more: 

```
> vctl describe myNginx
Name:                       myNginx
Status:                     running
Command:                    nginx -g daemon off;
Container rootfs in host:   /Users/mike/.vctl/storage/containerd/state/io.containerd.runtime.v2.task/vctl/myNginx/rootfs
IP address:                 192.168.243.128
Creation time:              2020-05-28T15:29:51-07:00
Image name:                 nginx:latest
Image size:                 48.7 MiB
Host virtual machine:       /Users/mike/.vctl/.r/vms/myNginx/myNginx.vmx
Container rootfs in VM:     /.containers/myNginx
Access in host VM:          vctl execvm --sh -c myNginx
Exec in host VM:            vctl execvm -c myNginx /bin/ls
```


### Exec into the container

vctl supports `exec`, meaning you can run commands in the container from the host. You can use this to run one-time commands, or to open an interactive shell. Also supports the **-d** flag to detach from the current terminal (i.e. whatever command you exec will run in the container but not display output to the current terminal)

Examples:

Interactivly:
```
> vctl exec -it myNginx sh
# ls
bin  boot  dev	etc  home  lib	lib64  media  mnt  opt	proc  root  run  sbin  srv  sys  tmp  usr  var
```

or:

```
> vctl exec myNginx ls
bin
boot
dev
etc
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
```

### Shell access into the container appliance VM

Nautilus has the ability to shell into the container appliance (virtual machine) of the specified container.

Example:

```
> vctl execvm --sh -c myNginx
sh-4.4#
```



### Keep the VM running after container stopped

By adding the "-k" parameter when running a container, when the container exits its appliance vm will keep running. You can still `vctl execvm --sh` into the container host to inspect logs and other debug info.
