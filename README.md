# Nitrux Update Tool System (`nuts`) rev. 0.0.1

## Introduction

The point of this utility is twofold, first, to be able to update the Nitrux Operating System. And second, to back up the root for rollbacks.

> _⚠️ Important: `nuts` is intended to work exclusively in Nitrux OS, and using this utility in other distributions will break them or not work at all. Please do not open issues regarding this use case; they will be closed._

## Usage

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
nuts version
```

* This command will display the version of `nuts`.


# Licensing

The license used for this repository and its contents is: BSD-3-Clause.

# Issues
If you find problems with the contents of this repository please create an issue.

©2023 Nitrux Latinoamericana S.C.
