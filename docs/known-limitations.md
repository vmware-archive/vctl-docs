# Current Known Limitations and Issues

### Limitations:
- Not all containers can run successfully now.  We are working toward support more container images. A list of containers can run successfully is provided [here](./support/image-support.md)

- Performance limitation.  With this tech preview, each container run in its own virtual machine, which provides better isolation from security perspective at cost of performance. 

- Nautilus will create a customized NAT vmnet. This will be shown in the Fusion Network Editor UI. It is not recomended to delete networks from the UI, rather let Nautilus handle them automatically. 

- Running containers may fail in nested environments (i.e. running Fusion within a macOS VM) and is not supported or tested.

- macOS administrator access is required to use the vctl cli. 'Standard' type users are not currently supported.

- IPv6 is not supported.

### Current Known Issues:

- After launching other version Fusion other than this TP build, $PATH will be reset and vctl can't be found without full path.

- - Resolution: Launch the TP version Fusion again before running vctl

- After the nautilus services are started (by running vctl system start), if the current user logs out, upon logging back in again the services will continue to run but will not be functional.

- - Resolution: run 'vctl system stop' and 'vctl system start' to restart the nautilus services


