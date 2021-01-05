# DDEV Remote Container Playground

In this repo, I try to setup a VS Code [Remote Container](https://code.visualstudio.com/docs/remote/containers-tutorial) for DDEV development on a remote host.

[https://github.com/microsoft/vscode-remote-try-php](vscode-remote-try-php) as used as a starting-point for this playground.

## Preparing the Host

I personally chose a Hetzner `CCX31` instance to host my development environment, running Ubuntu 20.04 and accessed as follows:

```
ssh://root@host-ip
```

First, SSH into the host and run the following code:

```
apt update
apt install -y docker.io
exit
```

## Preparing the Client

Install the [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension.

Then, in this workspace, run the following command:

```
mkdir .vscode
echo '{ "docker.host": "ssh://root@host-ip" }' > .vscode/settings.json
```
