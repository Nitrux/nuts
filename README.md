# Nitrux Update Tool System | [![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

<p align="center">
  <img width="128" height="128" src="https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/apps/64/nx-software-updater.svg">
</p>


# Introduction

We designed the Nitrux Update Tool System utility to update [Nitrux OS](https://nxos.org/) and to provide a rollback backup option.

> [!WARNING]
> We intended the Nitrux Update Tool System to work exclusively in Nitrux OS; using this utility in other distributions will break them or not work at all. Please do not open issues regarding this use case; they will be closed.

# Overview

The Nitrux Update Tool System is a simple, minimalistic system update and rollback utility. It performs three steps:

1. It creates a backup of the XFS partition using `xfsdump` and stores it locally.
2. Then, it downloads an [OTA-style](https://en.wikipedia.org/wiki/Over-the-air_update) archive and updates the system atomically.
3. Rollbacks are handled offline and integrated into the Nitrux ecosystem through the Live session using `xfsrestore`.

> [!NOTE]
> The Nitrux Update Tool System is included by default, starting with Nitrux 2.9.0.

---

### What the Nitrux Update Tool System is

- Minimalistic, focusing on necessary functionality.
- A CLI utility.
- [100% Free and Open Source Software](#licensing) written entirely in [POSIX-compliant scripting language](https://en.wikipedia.org/wiki/Shell_script#Typical_POSIX_scripting_languages).

### What the Nitrux Update Tool System is not

- A package manager.
  - The Nitrux Update Tool System does not interact with any binary software repository or package index, and does not manage packages. It has no "knowledge" about filesystem contents, cache, etc.
- An installer.
  - While we drew initial inspiration from the functional workflows of most Linux installers, they do not handle locale configuration, user management (including updating user settings), or partition configuration (e.g., modifying `/etc/fstab`), etc.
- Exclusively a backup utility.
  - The Nitrux Update Tool System is not designed exclusively as a general-purpose backup utility in the way that other CLI utilities like _restic_, _bup_, or filesystem-level tools like _xfsdump_ and _xfsrestore_, _btrfs-snapshot_, or _lvmcreate_ were.
    - To back up user data in Nitrux [use Kup](https://nxos.org/tutorial/how-to-create-backups-using-kup/).
- A container, virtual machine, Live USB creator, Linux distribution, desktop environment, or "proprietary software."
> [!NOTE]
> We don't know why anyone would think that, but one can never know, so let's clarify.

----

### Requirements

- Nitrux 2.8.0 and newer.
> [!NOTE]
> The utility will work out of the box starting with the mentioned release; however, the update files can set a minimum version.
- An active Internet connection.
> [!WARNING]
> The update process requires mandatory active internet connectivity via wired or wireless connections. Please connect to a functional network before updating. Additionally, your computer should be able to reach GitHub and the domain `raw.githubusercontent.com`.
- Depending on the update file size, up to 1.5 GB must be available in the home and root partitions.

### Misc. Information

The Nitrux Update Tool System can technically work with previous releases that use an immutable root, such as Nitrux 2.6.0, 2.6.1, 2.7.0, and 2.7.1, as long as the partition labels match the specific values (`NX_ROOT` for the root partition and `NX_HOME` for the home partition, which is standard since [Nitrux 2.8.0](https://nxos.org/changelog/release-announcement-nitrux-2-8-0/)), but they're not officially supported.

# Usage

We designed the Nitrux Update Tool System to be highly autonomous.

### Commands:

**Update**: `sudo nuts update`
- Updates the currently installed root using the specified archive in `nuts-query.info` and backs up the current root partition.

**Rescue**: `sudo nuts rescue`
- Restores the backup of the XFS root partition in case of an interrupted update.
> [!NOTE]
> The user can only use this operation from a Live session.

**Self-update**: `sudo nuts self-update`
- Updates the Nitrux Update Tool System and its configuration file using the default branch set in the configuration file.

### Configuration:

The Nitrux Update Tool System uses the file `/etc/nuts.conf` to load some settings.

### Options:

```
nuts -h or --help: Show this help.
nuts -v or --version: Show the version.
nuts -d or --debug: Enable verbose output.
nuts --use-main-branch: Defines the main branch of the Nitrux Update Tool System to download its components.
nuts --use-development-branch: Defines the development branch of the Nitrux Update Tool System to download its components.
```

# Licensing

The license for this repository and its contents is **BSD-3-Clause**.

# Issues

If you find problems with the contents of this repository, please create an issue and use the **🐞 Bug report** template.

## Submitting a bug report

Before submitting a bug, you should look at the [existing bug reports](https://github.com/Nitrux/nuts/issues) to verify that no one has reported the bug already.

©2023 Nitrux Latinoamericana S.C.
