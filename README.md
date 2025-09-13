# simple-ci

This is a small CI sytem for git repos.  

## Details

This CI consists of a git 'post-receive' hook, a worker script and a
systemd timer and scripts for automated updated rebuilds.

This is not meant to be used in big development environments for many users and
may not scale well for such environments.

This CI is entirely written as bash. All builds run in podman containers so
allowing own build scripts for the 'generic' pipeline are no security risk in my
opinion.

The runtime for a build is limited to 2 hours and the moory limit is 1GB for
now, then a still tunning container will be killed to avoid hanging workflow
containers hanging around.

**NOTE: You must have enabled lingering for the user which uses this ci.**

```sh
sudo loginctl enable-linger <USER>
```

## Prerequissites

On the host where the CI is installed you need to have at least podman installed
and running and you have to enable linger for the running user.

## Features

- In-repo build configuration files.
- No additional git repository solution neccessary.
- Can be run in any repository on any machine where you have ssh access to.
- Uses lock files to avoid concurrent builds of the same image to avoid race conditions.
- Runs in the (ssh) users context.
- Entirely written in bash.
- Highly extensible.
- Automatically integrates with FreeIPA and GSSAPI because it does generally not
  rely on external software for itself.
- Configurable remote host as a runner for a specific architecture. (Corrently
  out of the box supported are arm64, amd64 and riscv64)

## Trigger

Put an apropriate config file (see examples) in .simple-ci and name with the
branch you want to build as it`s name (e.g. master.conf).

## TODO (planned)

- [x] Support container builds on a podman remote host as runner for e.g. a
specific architecture.

- [x] Support git-crypt encrypted files in repositories.

- [x] Support build configurations using a custom configuration file.

- [x] Log the build process.

- [x] Support in-repo configuration.

- [x] Supports generic builds inside a container.

- [ ] Automatic tests of built container images.

- [ ] Implement some (semi) automatic versioning scheme and system, especially
for BootC Projects.
