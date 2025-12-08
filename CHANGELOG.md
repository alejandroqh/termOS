# Changelog

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.0] - 2025-12-08

### Added

#### Core System

- Alpine Linux-based minimal distribution (~5MB base)
- term39 (v0.18.0) as primary desktop environment
- Full-screen terminal multiplexer experience
- OpenRC init system
- greetd + tuigreet TUI login manager
- cage Wayland compositor for single-app display
- framebuffer mode support (80x50 inital, can be changed)

#### Architecture Support

- x86_64 architecture (PC, laptops)
  - EFI boot support with GRUB
  - BIOS boot support with extlinux/syslinux
- aarch64 architecture (ARM64)
  - Raspberry Pi 4/5 support / Laptops
  - ARM servers support
  - EFI boot with GRUB

#### Installation System

- Dialog-based TUI installer (termos-setup v2.0)
- Interactive disk selection menu
- Automated disk partitioning
  - EFI: GPT with 512MB EFI + root partition
  - BIOS: MBR with single bootable root partition
- Filesystem selection
  - ext4 (traditional, stable, recommended)
  - btrfs (modern, with @ and @home subvolumes, compression)
- Full disk encryption (LUKS2) for EFI systems
  - AES-XTS-PLAIN64 cipher
  - 512-bit key size
  - SHA-512 hash
  - Boot-time passphrase prompt with ASCII banner
- User account creation with sudo privileges
- Password-protected root account
- Automatic initramfs generation
- Hardware detection and module loading

#### Bootloader

- GRUB bootloader for EFI systems
  - Encryption support (copies kernel/initramfs to EFI partition)
  - btrfs subvolume support
  - Recovery mode option
  - 3-second timeout
- extlinux/syslinux for BIOS systems
  - Simple boot configuration
  - Recovery mode option
  - 30-second timeout
- Kernel update hooks for encrypted and btrfs systems

#### System Configuration

- NetworkManager for network management
- seatd session manager
- Hardware initialization scripts
  - Automatic module loading
  - Wireless device unblocking
  - XDG runtime directory setup
- System services auto-configuration
  - udev/eudev for hardware detection
  - localmount for filesystem mounting
  - greetd on tty2 (agetty on tty2 disabled)

#### Live Media

- Bootable ISO/USB installation media
- Console access for installation
- Boot media auto-detection (/media/cdrom compatibility)
- Local package repository on installation media
- Post-install automatic termos-base installation

#### Package System

- termos-aports repository structure
- term39 package (binary distribution from GitHub releases)
- termos-base meta-package with all dependencies
  - zsh shell
  - greetd + tuigreet
  - cage compositor
  - NetworkManager
  - mesa-dri-gallium (GPU drivers)
  - font-terminus
  - dosfstools, e2fsprogs, btrfs-progs
  - cryptsetup for encryption

#### Documentation

- Installation wizard with step-by-step dialogs
- ASCII art branding
- Welcome message (welcome.md)
- GPL compliance (LICENSE and SOURCES.txt included)
- CLAUDE.md project guidance for Claude Code

### Security

- LUKS2 full disk encryption with strong defaults
- User created with wheel group (sudo access)
- Root password protection
- Encrypted partition UUID-based mounting
- Boot-time encryption passphrase with visual banner

### Known Limitations

- Disk encryption only available on EFI systems (BIOS requires GRUB crypto which is not yet implemented)
- First-boot network configuration requires nmtui or NetworkManager
- Needs manual Time Zone setup

---

## Release Information

**Version:** 0.1.0
**Release Date:** December 8, 2025
**Status:** Initial Beta Release
**Architectures:** x86_64, aarch64
**Base:** Alpine Linux Edge
**Desktop:** term39 v0.18.0

### Checksums

ISO checksums will be provided with the release artifacts.

### Installation

Boot from ISO/USB and run:

```
termos-setup
```

Follow the interactive installation wizard.

### Testing

Tested on:

- UTM (macOS ARM64) - aarch64 native virtualization
- QEMU/KVM - x86_64 virtualization
- Physical hardware - x86_64 EFI and BIOS systems

---

[0.1.0]: https://github.com/yourusername/termos/releases/tag/v0.1.0
