# Nitrux Update Tool System (`nuts`)
[![Build and push packages to PackageCloud.](https://github.com/Nitrux/nuts/actions/workflows/build.yml/badge.svg)](https://github.com/Nitrux/nuts/actions/workflows/build.yml)

![](https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/apps/64/nx-software-updater.svg)


## Introduction

The point of this utility is twofold, first, to be able to update the Nitrux Operating System. And second, to back up the root for rollbacks.

> _⚠️ Important: `nuts` is intended to work exclusively in Nitrux OS, and using this utility in other distributions will break them or not work at all. Please do not open issues regarding this use case; they will be closed._

`nuts` targets Nitrux 2.6.0+.

### What is `nuts` (and what it isn't)

#### Overview

`nuts` is a simple (read. [KISS](https://people.apache.org/~fhanik/kiss.html)) system update and rollback utility.

#### What `nuts` is

 - `nuts` works by creating a backup of the current root directory using SquashFS; then, `nuts` downloads an ISO image, mounts it and uses `rsync` to update the installation. Afterward, when using `nuts` to restore a backup, `nuts` will do the exact process but use the locally generated SquashFS instead.

### What `nuts` is not

- `nuts` is not a package manager.
  - `nuts` does not interact with any sort of packaging format.
  - `nuts` does not interact with any software "repository" either.
- `nuts` is not an installer.
  - `nuts` is inspired by the functional workflow of most Linux installers, that is, extracting a SquashFS file. However, `nuts` does not handle in any way locale configuration, user creation, partition mounts, or bootloader configuration, etc.

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
