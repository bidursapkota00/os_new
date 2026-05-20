### GPT

- The first sector (LBA 0) of a GPT disk contains a Protective MBR.
- The Protective MBR exists for backward compatibility with legacy BIOS tools.
- It contains a single partition entry covering the entire disk, with a type code of 0xEE (GPT Protective).
- This prevents older MBR-only tools from treating the disk as unformatted and accidentally overwriting it.

- LBA 1 contains the Primary GPT Header.
- The GPT Header stores the disk's unique GUID, the location and size of the partition entry array, the number of partition entries, and CRC32 checksums for both the header and the partition entries.
- Starting from LBA 2, the next 32 sectors (LBA 2–33) contain the Partition Entry Array.
- Each partition entry is 128 bytes and contains a partition type GUID, a unique partition GUID, starting and ending LBA addresses, attribute flags, and a human-readable partition name (up to 36 UTF-16 characters).
- By default, the array supports up to 128 partition entries.

- Unlike MBR, GPT does not distinguish between primary and extended partitions; all 128 partitions are equal.
- There is no concept of an "active" partition in GPT. Instead, the UEFI firmware locates the EFI System Partition (ESP) by its well-known partition type GUID.
- The ESP is a FAT32-formatted partition that contains bootloader files (e.g., `\EFI\BOOT\BOOTX64.EFI`).

- When the computer is booted, UEFI firmware reads the GPT Header at LBA 1.
- It then reads the Partition Entry Array to find the EFI System Partition.
- The firmware loads and executes the bootloader from the ESP.
- The bootloader then loads the operating system.

- For reliability, GPT stores a backup copy of the header and partition entry array at the end of the disk.
- The backup GPT Header is stored in the last sector (last LBA) of the disk.
- The backup Partition Entry Array is stored in the 32 sectors just before the backup header.
- If the primary header or partition table is corrupted, the system can recover using the backup copy.

- GPT uses CRC32 checksums to detect corruption in the header and partition entries.
- If a checksum mismatch is found, the firmware can attempt to restore from the backup copy.

- Super block and free space management within each partition work the same as in MBR partitions, since those are file-system-level structures (e.g., ext4, NTFS) and are independent of the partitioning scheme.


LBA = Logical Block Address

GUID = Globally Unique Identifier

EFI = Extensible Firmware Interface

UEFI = Unified Extensible Firmware Interface

