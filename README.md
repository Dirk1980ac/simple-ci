# simple-ci

This is a small CI sytem for git repos.  
Actually it manages only automated container builds using podman.

## Details

This CI consists of a git 'post-receive' hook, a worker script and a
systemd timer and scripts for automated updated rebuilds.  

_*NOTE:*_ You must have enabled lingering for the user which uses this ci.

```sh
sudo loginctl enable-linger <USER>
```

## Triggers

* A build of a 'latest' tag is triggered on every commit to master branch.

* To avoid concurrent builds of the same image tag the Build is only triggered
if it is not already in progress using a simple "lock file".

## TODO (planned)

* Also compile other projects (which use autotools, meson, cmake...) and
eventually automatically build RPM packages.

* Automatic tests of built container images (if they are not bootc images).

* Report the success or failure of a build and it's ID in some manner.
