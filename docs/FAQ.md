# Project Nautilus FAQs

### How many containers can I run at the same time in my mac

This depends on your host memory and the nature of your container application. The container appliance only consumes as much memory as the services within it request

### How does vctl pass an entrypoint command to container

If no argument is passed to the 'vctl run container' command, by default the image's entrypoint command will be invoked.

 If there are arguments provided, unlike 'docker run' command where the arguments are appended to the image's predefined entrypoint command, in 'vctl run container', they themselves will be treated as the container's entrypoint command and replace the image's predefined one, to be invoked directly.


### How to reset my environment?

As a troubleshooting measure, you may choose to reset your container environment. 
Note that proceeding with the following steps, any container and image data will be lost.

```
> vctl system stop --force
```

This command will remove all existing container images and storage (use with caution!)

```
> rm -rf ~/.vctl 

> vctl system start
```
