# migrate-luks-hash

Tools to migrate a LUKS partition (created using the Whirlpool hash under `libgcrypt` < 1.6) to a different hash, per [this guide](https://wiki.gentoo.org/index.php?title=Sakaki%27s_EFI_Install_Guide/Migrating_from_Whirlpool_Hash_on_LUKS).

## Description

There is a [bug](https://bugs.archlinux.org/task/38550) in the implementation of the Whirlpool hash algorithm in versions < 1.6 of the `libgcrypt` library, as a result of which LUKS partitions created using it cannot be opened if the user subsequently migrates to version >= 1.6 (which has the correct implementation).

Accordingly, users who are affected by this will likely wish to migrate the hash function used in the LUKS header, using the `cryptsetup-reencrypt` command, as described [here](http://www.saout.de/pipermail/dm-crypt/2014-February/003956.html) and [here](https://wiki.gentoo.org/index.php?title=Sakaki%27s_EFI_Install_Guide/Migrating_from_Whirlpool_Hash_on_LUKS).

However, performing this migration requires that the LUKS partition in question be closed; so, if the system root is on there, then a temporary boot disk (with the appropriate <1.6 version of `libcrypt`) is needed, together with the `cryptsetup-reencrypt` utility itself.

This repository contains a suitable set of tools for this purpose.

> **Warning**: proceed at your own risk! Always make sure you have both LUKS header and content backups before attempting any modification of this type.

## Downloads

The following tools are provided as part of this package:

File | Description
:--- | :---
[install-amd64-minimal-20141113.iso](https://github.com/sakaki-/migrate-luks-hash/releases/download/1.0.0/install-amd64-minimal-20141113.iso) | Gentoo minimal install ISO from 13 November 2014 (includes the old `libgcrypt`, which is needed to open existing LUKS partitions that have been built with its (buggy) implementation of the Whirlpool hash algorithm. You can temporarily boot your PC using this (in MBR/CSM mode) when carrying out the LUKS header migration process.
[install-amd64-minimal-20141113.iso.CONTENTS](https://github.com/sakaki-/migrate-luks-hash/releases/download/1.0.0/install-amd64-minimal-20141113.iso.CONTENTS) | Contents listing for the above.
[install-amd64-minimal-20141113.iso.DIGESTS.asc](https://github.com/sakaki-/migrate-luks-hash/releases/download/1.0.0/install-amd64-minimal-20141113.iso.DIGESTS.asc) | Digests for the above two files, digitally signed by Gentoo release engineering.
[cryptsetup-reencrypt](https://github.com/sakaki-/migrate-luks-hash/releases/download/1.0.0/cryptsetup-reencrypt) | Dynamically linked version of the `cryptsetup-reencrypt` tool (suitable for use with the libraries on the minimal install ISO).
[cryptsetup-reencrypt.asc](https://github.com/sakaki-/migrate-luks-hash/releases/download/1.0.0/cryptsetup-reencrypt.asc) | Digital signature for the above tool (by me).

## Instructions

For full instructions, please see [this Gentoo Wiki article](https://wiki.gentoo.org/index.php?title=Sakaki%27s_EFI_Install_Guide/Migrating_from_Whirlpool_Hash_on_LUKS).

## Feedback Welcome!

If you have any problems, questions or comments regarding this project, feel free to drop me a line! (sakaki@deciban.com)
