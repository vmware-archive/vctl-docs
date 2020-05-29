# VMware Project Nautilus
Project and doc repo for VMware Project Nautilus


## What is Project Nautilus?

Project Nautilus is the name ascribed to an ongoing transformation of Fusion and Workstation to support OCI Containers, and more. Under the project we have developed 'vctl', whcih allows Fusion to push, pull, and natively run docker and oci-compliant contaniner images and kubernetes clusters on developer workstations. (Coming soon: 'build' images from dockerfile, and Workstation support.)


## How do I install vctl?

'vctl' is included with Fusion 11.5.5 and the 20H2 Tech Preview of VMware Fusion. The 'vctl' command line tool is added to $PATH by default each time Fusion starts, and does not need tobe installed seperately.


## Where can I try Fusion 11.5.5?
Fusion includes a built-in 30 day trial license.

You can download it directly from here:

- [vmware.com/go/getfusion](https://vmware.com/go/getfusion)

## Where do I get the Fusion 20H2 Tech Preview?

You can download the beta from here: ***[https://bit.ly/getnautilus](https://bit.ly/getnautilus)***


## Can I have Fusion and Fusion Tech Preview installed at the same time?

Yes. Fusion dynamically loads kernel extensions when it launches and unloads them when it quits, so it will always load the right backend services for the version you're trying to start.


## Can I run Fusion and Fusion Tech Preview at the same time?

No. You should quit VMware Fusion non-tech preview version before launching the Tech Preview build.


## How do I use Nautilus?

Nautilus is the sum of two main parts: The 'engine' and backend runtime support services, and the front-end CLI. Users interact with Nautilus using the 'vctl' command to start services, and perform operations with containers. Our backend is based on containerd, so if your application can communicate with the containerd daemon, we hope it would work with ours as well. 


## What are the System Requirements?

Fusion 20H2 Tech Preview requires macOS 10.14 as a minimum host OS.

Fusion 11.5.5 system requirements have unchagned since as of 15.5.0


## How do I get started?

You can check out our Getting Started guide ***[here](./docs/getting-started.md)***








