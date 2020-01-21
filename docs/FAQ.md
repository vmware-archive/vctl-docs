### How many containers can I run at the same time in my mac

This depends on your host memory. The default memory size for each PodVM is 1G. You can use vctl system prepare to change this default configuration.

### How does vctl pass an entrypoint command to container

If no argument is passed to the 'vctl run container' command, by default the image's entrypoint command will be invoked.

 If there are arguments provided, unlike 'docker run' command where the arguments are appended to the image's predefined entrypoint command, in 'vctl run container', they themselves will be treated as the container's entrypoint command and replace the image's predefined one, to be invoked directly.


### How to reset Nautilus?

As a troubleshooting measure, you may choose to reset Nautilus. 
Note that proceeding with the following steps, any container and image data will be lost.

```
% vctl system stop
```

Warning: Don't save any other data under ~/.nautilus, or back ~/.nautilus before running next command.

```
% rm -rf ~/.nautilus 

% vctl system start
```

### How to completely remove Project Nautilus data after removing Fusion Tech Preview 20H1

Your environment can be cleaned up with the following steps:

```
% vctl system stop
```
Remove Fusion Tech Preview by dragging it to the trash

Then remove the Nautilus container image and config folder.

```
% rm -rf ~/.nautilus  
```
