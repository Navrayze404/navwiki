# Disk Preparation

Before installing Nav Linux, you need to prepare a destination partition. The installation process depends on whether your system already has an EFI System Partition (ESP) and a swap partition.

## Check Available Disks

First, list all available storage devices and partitions.

```bash
lsblk -o NAME,SIZE,TYPE,FSTYPE,MOUNTPOINT
```

Example:

```text
NAME   SIZE TYPE FSTYPE MOUNTPOINT
sda   931.5G disk
├─sda1 260M part vfat
├─sda2  16M part
├─sda3 931G part ntfs

sdb   931.5G disk
├─sdb1 512M part vfat
├─sdb2  16G part swap
├─sdb3 100G part ntfs
└─sdb4 815G part ntfs

sdc    16G disk
└─sdc1  16G part vfat /run/initramfs/live
```

> In this example:
>
> - `/dev/sdc` is the Nav Linux Live USB.
> - `/dev/sdb` is the installation target.

---

# Scenario 1 — Existing EFI and Swap Partitions

Choose this option if:

- Windows is already installed in UEFI mode.
- An EFI System Partition already exists.
- A swap partition already exists.

You only need to prepare a root partition for Nav Linux.

Format the root partition:

```bash
mkfs.ext4 -F /dev/sdb3
```

Mount the root partition:

```bash
mount /dev/sdb3 /mnt
```

Mount the existing EFI partition:

```bash
mkdir -p /mnt/boot/efi
mount /dev/sdb1 /mnt/boot/efi
```

Enable the existing swap partition:

```bash
swapon /dev/sdb2
```

Verify the mounted partitions:

```bash
findmnt /mnt
swapon --show
```

Continue to **Installing Nav Linux**.

---

# Scenario 2 — No EFI or Swap Partitions

Choose this option if:

- The disk is empty.
- No operating system is installed.
- No EFI System Partition exists.
- No swap partition exists.

## Create the Partition Table

Launch `cfdisk`:

```bash
cfdisk /dev/sdb
```

Create the following partitions:

| Partition | Size | Type |
|-----------|------|------|
| EFI System Partition | 512 MiB | EFI System |
| Swap | 8–16 GiB | Linux swap |
| Root | Remaining Space | Linux filesystem |

Write the changes and exit.

## Format the Partitions

Format the EFI partition:

```bash
mkfs.fat -F32 /dev/sdb1
```

Format the root partition:

```bash
mkfs.ext4 -F /dev/sdb3
```

Initialize the swap partition:

```bash
mkswap /dev/sdb2
```

Activate swap:

```bash
swapon /dev/sdb2
```

Mount the root partition:

```bash
mount /dev/sdb3 /mnt
```

Mount the EFI partition:

```bash
mkdir -p /mnt/boot/efi
mount /dev/sdb1 /mnt/boot/efi
```

Verify the installation target:

```bash
findmnt /mnt
swapon --show
```

Continue to **Installing Nav Linux**.
