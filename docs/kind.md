# Using kind with vctl

VMware Fusion 12 and Workstation 16, Pro and Player, both ship with the ability for 'vctl' to be used to deploy kind based kubernetes clusters.

The way vctl implements this is by creating an alias to the docker CLI used by kind to manage the lifecycle of the cluster. From there, kind handles all the rest.

## How to use
Firstly, make sure the container runtime has been started:

`> vctl system start`

Once the runtime has started, use the following command:

`> vctl kind`

The output should look like this:
```
> vctl kind
Downloading 3 files...
Downloading [crx.vmdk 38.59% kubectl 86.57% kind-darwin-amd64 1.56%]
Finished kubectl 100.00%
Downloading [crx.vmdk 64.98% kind-darwin-amd64 40.06%]
Finished kind-darwin-amd64 100.00%
Downloading [crx.vmdk 93.05%]
Finished crx.vmdk 100.00%
3 files successfully downloaded.

vctl-based KIND is ready now. KIND will run local Kubernetes clusters by using vctl containers as "nodes"

* All Docker commands have been aliased to vctl in the current terminal. Docker commands performed in current window would be executed through vctl.
```

`vctl kind` does 2 things:
1) It downloads the necessary components if they are not present

    - kubectl
    - kind for macOS
    - the 'crx' virtual appliance container host environment, specifically tuned for `kind`

2) It creates an alias of the docker executable to instead use 'vctl'.
``` 
> which docker 
/Users/mike/.vctl/bin/docker
```
## Okay, now what?

From here, the rest is standard [kind operations](https://kind.sigs.k8s.io/docs/user/quick-start/).

For example, you can create a basic cluster with:

`> kind create cluster`

## Loading an image into a kind cluster

vctl supports auto-loading of a container image into an existing kind cluster at build time.
what this means is you can use the following:

`> vctl build -t image:tag --kind-load .`

If you have already pulled the image from some place, instead of bulding it directly, you can use the `kind load docker-image` command:

`> kind load docker-image image:tag`

Once the image is in the cluster, you can run it directly, or apply a .yaml file that uses that image.

`> kubectl run --image image:tag --restart=Never --image-pull-policy=Never my-pod-name`



