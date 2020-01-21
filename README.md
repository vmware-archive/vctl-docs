# VMware Project Nautilus
Project and doc repo for VMware Project Nautilus


## What is Project Nautilus?

Taking inspiration from the Kubernetes community, Project Nautilus allows Fusion and Workstation to push, pull, and natively run docker and oci-compliant contaniner images and kubernetes clusters on developer workstations.

Project Nautilus is also an ongoing effort within VMware to reshape how Fusion and Workstation are used to develop and test applications.


## How do I install Nautilus?

Nautilus is included with the 20H1 Tech Preview of VMware Fusion. The 'vctl' command line tool is added to $PATH by default and can be used once Fusion Tech Preview is installed.


## Where do I get the Fusion 20H1 Tech Preview?

You can download the beta from here: ***https://bit.ly/getnautilus***


## Can I have Fusion and Fusion Tech Preview installed at the same time?

Yes. Fusion dynamically loads kernel extensions when it launches and unloads them when it quits, so it will always load the right backend services for the version you're trying to start.


## Can I run Fusion and Fusion Tech Preview at the same time?

No. You should quit VMware Fusion non-tech preview version before launching the Tech Preview build.


## How do I use Nautilus?

Nautilus is the sum of two main parts: The 'engine' and backend runtime support services, and the front-end CLI. Users interact with Nautilus using the 'vctl' command to start services, and perform operations with containers.


## What are the System Requirements?

To support Nautilus, Fusion 20H1 Tech Preview requires macOS 10.14 as a minimum host OS.


## How do I get started?

You can check out our Getting Started guide ***[here](https://github.com/VMwareFusion/nautilus/blob/master/docs/getting-started.md)***








