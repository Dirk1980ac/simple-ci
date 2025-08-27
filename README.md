# simple-ci

This is a small CI sytem for git repos.  
Actually it manages only automated container builds using podman.

## Details

This CI consists of a git 'post-receive' hook, a worker script and a
systemd timer and scripts for automated updated rebuilds.  

**NOTE: You must have enabled lingering for the user which uses this ci.**

```sh
sudo loginctl enable-linger <USER>
```

## Features

* No additional git repository solution neccessary.
* Can be run in any repository on any machine where you have ssh access to.
* Uses lock files to avoid concurrent builds of the same image to avoid race conditions.
* Runs in the (ssh) users context so it is useful for single developers as well
as for Teams

* Entirely written in bash
* Highly extensible.
* Automatically integrates with FreeIPA and GSSAPI because it does generally not
rely on external software for itself.
* Configurable remote host as a runner for a specific architecture. (Corrently
out of the box supported are arm64, amd64 and riscv64)

## Triggers

* A build of a 'latest' tag is triggered on every commit to master branch.

## TODO (planned)

* [x] Support container builds on a podman remote host as runner for e.g. a
specific architecture.

* [ ] Also compile other projects (which use autotools, meson, cmake...) and
eventually automatically build RPM packages.

* [ ] Automatic tests of built container images (if they are not bootc images).

* [ ] Report the success or failure of a build and it's ID in some manner.
