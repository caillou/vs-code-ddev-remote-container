# DDEV Remote Container Playground

In this repo, I try to setup a VS Code [Remote Container](https://code.visualstudio.com/docs/remote/containers-tutorial) for DDEV development on a remote host.

## Preparing the Host

I personally chose a Hetzner `CCX31` instance to host my development environment, running Ubuntu 20.04 and accessed as follows:

```
ssh://root@host
```

First, SSH into the host and run the following code:

```
apt update
apt install -y docker.io
```
