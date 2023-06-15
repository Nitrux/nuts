# Nitrux Update Tool System (`nuts`)

![](https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/apps/64/nx-software-updater.svg)


# Introduction

The Nitrux Update Tool System (`nuts`) utility is designed to update [Nitrux OS](https://nxos.org/) and provide a backup option for rollbacks.

> _⚠️ Important: `nuts` is intended to work exclusively in Nitrux OS, and using this utility in other distributions will break them or not work at all. Please do not open issues regarding this use case; they will be closed._


## Requeriments

- Nitrux 2.8.0+.
  - _`nuts` is included by default starting with Nitrux 2.9.0._
- An active Internet connection.
- Up to 1.6 GB of available space in the root partition and more than 3.2 GB in the home partition.


### Support for Previous Releases

`nuts` can technically work with previous releases that use an immutable root, such as Nitrux 2.6.0, 2.6.1, 2.7.0, and 2.7.1, as long as the partition labels match the specific values (`NX_ROOT` for the root partition and `NX_HOME` for the home partition).

To see the partition label run the command `blkid`.

**How to go `nuts` on Previous Releases**

For releases of Nitrux where `nuts` is not available by default, do the following.

```
git clone --depth=1 https://github.com/Nitrux/nuts.git $HOME/nuts
sudo cp $HOME/nuts/usr/bin/nuts /usr/bin
sudo cp $HOME/nuts/nuts.conf /etc
```

# Overview

`nuts` is a simple and minimalistic system update and rollback utility. It performs three steps:

1. Creates a backup of the current root directory using SquashFS.
2. Downloads the latest ISO image using the BitTorrent protocol and updates the system using `rsync`.
3. When restoring a backup, `nuts` uses the locally generated SquashFS file instead of downloading.


#### What `nuts` is

- Minimalistic, focusing on necessary functionality.
- A CLI utility.
- 100% Free and Open Source Software written entirely in [POSIX-compliant scripting language](https://en.wikipedia.org/wiki/Shell_script#Typical_POSIX_scripting_languages).

#### What `nuts` is not

- A package manager.
  - `nuts` does not interact with any sort of packaging format.
  - `nuts` does not interact with any software "repository" either.
  - `nuts` does not interact with any package manager to perform any operation.
- An installer.
  - `nuts` is inspired by the functional workflow of most Linux installers, that is, extracting a SquashFS file. However, `nuts` does not handle in any way locale configuration, user creation, partition mounts, or bootloader configuration, etc.
- Solely a backup utility.
  - `nuts` is not designed exclusively as a backup utility in the way that other utilities like _restic_, _bup_ or filesystem-level tools like _xfsdump_ and _xfsrestore_, _btrfs-snapshot_ or _lvmcreate_ were.
- A container, virtual machine, Live USB creator, Linux distribution, or desktop environment.
  - _**Note**: We don't know why anyone would think that, but one can never know, so let's clarify that._

# Usage

`nuts` is designed to be highly autonomous.

### Commands:

**Update**: `sudo nuts update`
- Updates the currently installed root using the specified media in nuts-query and backs up the current root directory.

**Restore**: `sudo nuts restore`
- Restores the backup of the root directory generated during the update.

### Configuration:

`nuts` uses the file `/etc/nuts/nuts.conf` to load some settings.

### Options:

- `sudo nuts -h`: Displays the help of `nuts`.
- `sudo nuts -d`: Runs `nuts` in verbose mode.
- `sudo nuts -v`: Displays the version of `nuts`.

# Licensing

The repository and its contents are licensed under BSD-3-Clause.

# Issues
If any problems are encountered, users can create an issue.

©2023 Nitrux Latinoamericana S.C.
