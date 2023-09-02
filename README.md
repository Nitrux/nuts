# Nitrux Update Tool System (`nuts`) | [![License](https://img.shields.io/badge/License-BSD_3--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

<p align="center">
  <img width="128" height="128" src="https://raw.githubusercontent.com/Nitrux/luv-icon-theme/master/Luv/apps/64/nx-software-updater.svg">
</p>


# Introduction

The Nitrux Update Tool System (`nuts`) utility is designed to update [Nitrux OS](https://nxos.org/) and provide a backup option for rollbacks.

> _⚠️ Important: `nuts` is intended to work exclusively in Nitrux OS, and using this utility in other distributions will break them or not work at all. Please do not open issues regarding this use case; they will be closed._

# Overview

`nuts` is a simple and minimalistic system update and rollback utility. It performs three steps:

1. Creates a backup of the root directory using SquashFS and the XFS partition and stores them locally.
2. Downloads the latest ISO image using the BitTorrent protocol and updates the system using `rsync`.
3. When restoring a backup, use the locally generated SquashFS file (instead of downloading an ISO).

> _♦ Information: `nuts` is included by default starting with Nitrux 2.9.0._

---

### What `nuts` is

- Minimalistic, focusing on necessary functionality.
- A CLI utility.
- [100% Free and Open Source Software](#licensing) written entirely in [POSIX-compliant scripting language](https://en.wikipedia.org/wiki/Shell_script#Typical_POSIX_scripting_languages).

### What `nuts` is not

- A package manager.
  - `nuts` does not interact with any sort of packaging format.
  - `nuts` does not interact with any software "repository" either.
  - `nuts` does not interact with any package manager to perform any operation.
- An installer.
  - `nuts` is inspired by the functional workflow of most Linux installers, that is, extracting a SquashFS file. However, `nuts` does not handle in any way locale configuration, user creation, user management (including updating user settings, i.e., updating Latte Dock, Plasma, or ZSH configuration), partition configuration (such as modifying /etc/fstab), or bootloader configuration (such as modifying /etc/default/grub), etc.
- Solely a backup utility.
  - `nuts` is not designed exclusively as a backup utility in the way that other utilities like _restic_, _bup_ or filesystem-level tools like _xfsdump_ and _xfsrestore_, _btrfs-snapshot_ or _lvmcreate_ were. To backup user data in Nitrux [use Kup](https://nxos.org/tutorial/how-to-create-backups-using-kup/).
- A container, virtual machine, Live USB creator, Linux distribution, desktop environment, or "proprietary software."
  - _**Note**: We don't know why anyone would think that, but one can never know, so let's clarify that._

----

### Requirements

- Nitrux 2.8.0+.
- An active Internet connection.
- Up to 1.6 GB of available space in the root partition and more than 3.2 GB in the home partition.

### Support for Previous Releases

`nuts` can technically work with previous releases that use an immutable root, such as Nitrux 2.6.0, 2.6.1, 2.7.0, and 2.7.1, as long as the partition labels match the specific values (`NX_ROOT` for the root partition and `NX_HOME` for the home partition which is standard since [Nitrux 2.8.0](https://nxos.org/changelog/release-announcement-nitrux-2-8-0/)).

To see the partition label run the command `blkid`.

**How to go `nuts` on Previous Releases**

For releases of Nitrux where `nuts` is not available by default, do the following.

```
git clone --depth=1 https://github.com/Nitrux/nuts.git $HOME/nuts
sudo cp $HOME/nuts/usr/bin/nuts /usr/bin
sudo cp $HOME/nuts/etc/nuts.conf /etc
```

# Usage

`nuts` is designed to be highly autonomous.
   - _♦ Information: The use of this utility requires `sudo`_

### Commands:

**Update**: `nuts update`
- Updates the currently installed root using the specified media in `nuts-query` and backs up the current root directory and partition.

**Restore**: `nuts restore`
- Restores the backup of the root directory generated during the update.

**Rescue**: `nuts rescue`
- Restores the backup of the XFS root partition in case of an interrupted update.
   - _♦ Information: This operation is a special handling of an unforeseen event. If rsync were to be interrupted, the root would be inconsistent. That means the root is unusable, i.e., the user can't access the GUI or, worse, a TTY, so the user can't restore the SquashFS. This operation will allow the user to restore the root partition from a Live session. This operation does not replace `restore`; it exists if using `restore` is impossible._

### Configuration:

`nuts` uses the file `/etc/nuts.conf` to load some settings.

### Options:

```
nuts -h: Displays the help of nuts.
nuts -d: Runs `nuts` in verbose mode.
nuts -v: Displays the version of nuts.
```

# Updating the Nitrux Update Tool System

Whenever a new update to the utility is uploaded to the repository, users must do the following to update the utility itself.

```
sudo overlayroot-chroot
mount -t devtmpfs dev /dev

#   Clone repository
git clone --depth=1 https://github.com/Nitrux/nuts.git /nuts

#   Copy nuts and its config file to the root
cp /nuts/usr/bin/nuts /usr/bin
cp /nuts/etc/nuts.conf /etc

#   Optionally delete /nuts
rm -r /nuts

umount /dev
exit

#   Reboot to load the changes to the overlay
sudo reboot
```

# Licensing

The repository and its contents are licensed under **BSD-3-Clause**.

# Issues
If any problems are encountered, users can create an issue.

©2023 Nitrux Latinoamericana S.C.
