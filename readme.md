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
apt install -y docker.io zsh
useradd -m -s /bin/zsh -u 1000 node
mkdir /home/node/workspace
chown 1000:1000 /home/node/workspace
exit
```

## Preparing the Client

Install the [Remote Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension.

Then, in this workspace, run the following command:

```
mkdir .vscode
echo '{ "docker.host": "ssh://root@host-ip" }' > .vscode/settings.json
```

...

Once the container has started, you can initialize your dev environment.

First, we generate a new ssh key to use with our git repository:

```
ssh-keygen -f ~/.ssh/id_rsa -t rsa -N ''
ssh-add ~/.ssh/id_rsa
more ~/.ssh/id_rsa.pub
```

Add the newly generated public key to your repository profile.
