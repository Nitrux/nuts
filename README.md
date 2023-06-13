# Nitrux Update Tool System (`nuts`)
[![Build and push packages to PackageCloud.](https://github.com/Nitrux/nuts/actions/workflows/build.yml/badge.svg)](https://github.com/Nitrux/nuts/actions/workflows/build.yml)

![](https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/apps/64/nx-software-updater.svg)


## Introduction

The point of this utility is twofold, first, to be able to update the Nitrux Operating System. And second, to back up the root for rollbacks.

`nuts` targets Nitrux 2.6.0+.

> _⚠️ Important: `nuts` is intended to work exclusively in Nitrux OS, and using this utility in other distributions will break them or not work at all. Please do not open issues regarding this use case; they will be closed._


### What is `nuts` (and what it isn't)

#### Overview

`nuts` is a simple (read. [KISS](https://people.apache.org/~fhanik/kiss.html)) system update and rollback utility.

`nuts` works in three steps. First by creating a backup of the current root directory using SquashFS; then, `nuts` downloads an ISO image using the BitTorrent protocol, and uses `rsync` to update the system. 

Afterward, when using `nuts` to restore a backup, `nuts` will do the exact process but use the locally generated SquashFS instead, so, no downloads.

#### What `nuts` is ✅

 - `nuts` is minimalistic.
   - `nuts` was designed to only do what it needs to do and nothing else.
   - `nuts` is a CLI utility.
- `nuts` is 100% Free (as in Freedom) Open Source Software; see [License](#licensing).
- `nuts` is written entirely in [POSIX-compliant scripting language](https://en.wikipedia.org/wiki/Shell_script#Typical_POSIX_scripting_languages).

#### What `nuts` is not ❎

- `nuts` is not a package manager.
  - `nuts` does not interact with any sort of packaging format.
  - `nuts` does not interact with any software "repository" either.
  - `nuts` does not interact with any package manager to perform any operation.
- `nuts` is not an installer.
  - `nuts` is inspired by the functional workflow of most Linux installers, that is, extracting a SquashFS file. However, `nuts` does not handle in any way locale configuration, user creation, partition mounts, or bootloader configuration, etc.
- `nuts` is not "only" a backup utility.
  - `nuts` is not designed exclusively as a backup utility in the way that other utilities like _restic_, _bup_ or filesystem-level tools like _xfsdump_ and _xfsrestore_, _btrfs-snapshot_ or _lvmcreate_ were.
- `nuts` is not a container or a virtual machine, or a utility to make Live USBs, a Linux distribution, a desktop environment, etc.; see [Overview](#overview).
  - _**Note**: We don't know why anyone would think that, but one can never know, so let's clarify that._

## Usage

This utility is designed to be highly autonomous.

To use `nuts`, do the following.

Open a terminal and run one of the following commands.

### Update

```
sudo nuts update
```

* The command above will update the currently installed root using the media specified in `nuts-query` and backup the current root directory.

### Restore
```
sudo nuts restore
```

* The command above will restore the backup of the root directory generated during the update.

### Configuration

This utility is not designed to be highly configurable.

However, `nuts` uses the file in `/etc/nuts/nuts.conf` to load some settings.

### Options

This utility is not designed to be highly interactive.

```
sudo nuts -h
```

* This command will display the help of `nuts`.


# Licensing

The license used for this repository and its contents is: BSD-3-Clause.

# Issues
If you find problems with the contents of this repository please create an issue.

©2023 Nitrux Latinoamericana S.C.
