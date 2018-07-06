# Snap of sshguard

[![Snap Status](https://build.snapcraft.io/badge/tsunghanliu/sshguard.snap.svg)](https://build.snapcraft.io/user/tsunghanliu/sshguard.snap)

**This snap is NOT official.** That's why there is a postfix string `-robertliu` appended to the snap name.

[sshguard](https://www.sshguard.net/) protects hosts from brute-force attacks against SSH and other services. It aggregates system logs and blocks repeat offenders using one of several firewall backends, including iptables, ipfw, and pf.

Although sshguard supports ipfw, pf and other firewall backends, this snap only enables the iptables backend in this snap.

# Build

To build the snap, you have to use *snapcraft*. Read the official [document](http://snapcraft.io/docs/build-snaps/) for the details. This command will produce a file named `sshguard_<ver>_<arch>.snap`. `<ver>` means the version number and `<arch>` stands for the architecture of target machines.

```
$ snapcraft snap
```

# Installation

## Install snapd

### Ubuntu Core

Please read the official [document](https://developer.ubuntu.com/core/get-started) and install Ubuntu Core onto your hardware.

### Ubuntu Desktop / Server

There are good tutorials for beginers on [Ubuntu tutorials](https://tutorials.ubuntu.com/). You can refer to the tutorials for both [desktop](https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-desktop#0) and [server](https://tutorials.ubuntu.com/tutorial/tutorial-install-ubuntu-server#0).

### Other Linux distributions

Please check the [installation guides](https://docs.snapcraft.io/core/install) on http://snapcraft.io and see how to enable the snappy environment on other Linux distributions.

## Install sshguard snap

Each snap has a revision (`<rev>`). A snap installed from the store always has a revision in number. But the revision of a local snap has a lead 'x'.

### Use Ubuntu store

There are four channels used to control or track different version/revision. Please refer to the [document](https://docs.snapcraft.io/reference/channels). The following command uses the stable channel which is the default value.

```console
$ sudo snap install sshguard-robertliu
```

### Use local snap

Upload the snap file to your target machine then install it.

```console
$ sudo snap install --dangerous sshguard-robertliu_<ver>_<arch>.snap
```

## Configure interfaces

These interfaces **MUST** be correctly configured, otherwise the services will not start successfully.

```console
$ sudo snap connect sshguard-robertliu:firewall-control
$ sudo snap connect sshguard-robertliu:log-observe
$ sudo snap restart sshguard-robertliu
```

## Configure sshguard

The configuration file is at `/var/snap/sshguard-robertliu/<rev>/sshguard.conf`.
Please check the [official document](https://www.sshguard.net/docs/) to understand the parameters.

## Add whitelist IP addresses or domain names

The whitelist is placed at `/var/snap/sshguard-robertliu/<rev>/whitelist`.

```console
$ sudo vi /var/snap/sshguard-robertliu/<rev>/whitelist
# edit and save it
```

# Service logs

To get the logs of sshguard snap, please use the command
```console
$ sudo snap logs sshguard-robertliu.sshguard
```

# Backup, upgrade and restore

Configuration files and log files are store at `/var/snap/sshguard-robertliu/<rev>/`, To modify or backup your configurations, you can backup the whole directory, or just pick some of files.
```console
$ sudo cp /var/snap/sshguard-robertliu/<rev>/sshguard.conf $HOME
$ sudo cp /var/snap/sshguard-robertliu/<rev>/whitelist $HOME
```

Snapd will refresh snaps automatically by default. If you want to do it manually, use this command:
```console
$ sudo snap refresh sshguard-robertliu
```

To restore the settings, copy the file to the `/var/snap/sshguard/<rev>/`
```console
# restore configuration files
$ sudo cp $HOME/sshguard.conf /var/snap/sshguard-robertliu/<rev>/
$ sudo cp $HOME/whitelist /var/snap/sshguard-robertliu/<rev>/
# restart services
$ sudo snap restart snap.sshguard-robertliu.sshguard
```

# Uninstall sshguard snap

To remove this snap

```console
$ sudo snap remove sshguard-robertliu
```

# Bug reports and feedback

Please use the [github issues page](https://github.com/tsunghanliu/sshguard.snap/issues) to report any problems and suggestions.

# Known issues

* N/A

