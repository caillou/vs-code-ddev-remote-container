# DDEV Remote Container Playground

In this repo, I try to setup a VS Code [Remote Container](https://code.visualstudio.com/docs/remote/containers-tutorial) for DDEV development on a remote host.

[https://github.com/microsoft/vscode-remote-try-php](vscode-remote-try-php) as used as a starting-point for this playground.

## Todo

- [ ] Start `dockerd` when the container starts.
- [ ] Fix the following `ddev` build error (`/var/www/html/app/var` is `root`):
  ```
  Fatal error: Uncaught RuntimeException: Could not create directory "/var/www/html/app/var/log/"! in /var/www/html/app/public/typo3/sysext/core/Classes/Utility/GeneralUtility.php:2047
  Stack trace:
  #0 /var/www/html/app/public/typo3/sysext/core/Classes/Utility/GeneralUtility.php(2015): TYPO3\CMS\Core\Utility\GeneralUtility::createDirectoryPath('/var/www/html/a...')
  #1 /var/www/html/app/public/typo3/sysext/core/Classes/Log/Writer/FileWriter.php(226): TYPO3\CMS\Core\Utility\GeneralUtility::mkdir_deep('/var/www/html/a...')
  #2 /var/www/html/app/public/typo3/sysext/core/Classes/Log/Writer/FileWriter.php(192): TYPO3\CMS\Core\Log\Writer\FileWriter->createLogFile()
  #3 /var/www/html/app/public/typo3/sysext/core/Classes/Log/Writer/FileWriter.php(122): TYPO3\CMS\Core\Log\Writer\FileWriter->openLogFile()
  #4 /var/www/html/app/public/typo3/sysext/core/Classes/Log/Writer/FileWriter.php(81): TYPO3\CMS\Core\Log\Writer\FileWriter->setLogFile('/var/www/html/a...')
  #5 /var/www/html/app/public/typo3/sysext/core/Classes/Utility/GeneralUtility.php in /var/www/html/app/public/typo3/sysext/core/Classes/Utility/GeneralUtility.php on line 2047
  ```
- [ ] Automatically generate and persist `ssh` keys on first start.
- [ ] Persist `zsh` history.

## Preparing the Host

I personally chose a Hetzner `CCX31` instance to host my development environment, running Ubuntu 20.04 and accessed as follows:

```
ssh://root@host-ip
```

First, SSH into the host and run the following code:

```
apt update
apt install -y docker.io zsh
wget https://github.com/nestybox/sysbox/releases/download/v0.2.1/sysbox_0.2.1-0.ubuntu-focal_amd64.deb
apt install -y linux-headers-$(uname -r)
apt install ./sysbox_0.2.1-0.ubuntu-focal_amd64.deb -y
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
