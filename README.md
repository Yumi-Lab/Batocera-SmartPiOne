<p align="center">
  <a href="https://batocera.org/">
    <img src="assets/logo_batocera.png" alt="Batocera Linux" height="80"/>
  </a>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://www.yumi-lab.com">
    <img src="assets/logo_yumi.png" alt="Yumi Lab" height="80"/>
  </a>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://batocera.org/">
    <img src="assets/logo_batocera.png" alt="Batocera Linux" height="80"/>
  </a>
</p>

# Batocera-SmartPiOne

[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=plastic)](https://github.com/Yumi-Lab/Batocera-SmartPiOne/blob/master/COPYING)
[![Version](https://img.shields.io/badge/Version-v38-green?style=plastic)](https://github.com/Yumi-Lab/Batocera-SmartPiOne/releases)
[![Downloads](https://img.shields.io/github/downloads/Yumi-Lab/Batocera-SmartPiOne/total?style=plastic)](https://github.com/Yumi-Lab/Batocera-SmartPiOne/releases)
[![Wiki](https://img.shields.io/badge/Wiki-batocera.org-orange?style=plastic&logo=gitbook&logoColor=white)](https://wiki.batocera.org/)

Turn your SmartPi One into a plug-and-play retrogaming console — **117 systems**, RetroAchievements, scraper, gamepad auto-detection — powered by **[Batocera Linux](https://batocera.org/)**.

> This is a fork of [batocera-linux/batocera.linux](https://github.com/batocera-linux/batocera.linux) with SmartPi One board support added.

## Table of Contents

- [Supported Hardware](#supported-hardware)
- [Quick Start](#quick-start)
- [Features](#features)
- [Emulation Performance](#emulation-performance)
- [Supported Systems (117)](#supported-systems-117)
- [What We Changed](#what-we-changed-from-upstream-batocera)
- [Build from Source](#build-from-source)
- [Roadmap](#roadmap)
- [Related Projects](#related-projects)
- [Documentation](#documentation)
- [License](#license)

## Supported Hardware

### SmartPi One
![SmartPi One](https://img.shields.io/badge/SmartPi_One-Allwinner_H3-orange?style=plastic&logo=arm&logoColor=white)

| Specification | Value |
|---------------|-------|
| **SoC** | Allwinner H3 — Cortex-A7 quad-core @ 1.0 GHz |
| **RAM** | 1 GB DDR3 (576 MHz, custom tuning) |
| **GPU** | Mali-400 MP2 — Lima / Mesa (GLES 2.0) |
| **WiFi** | Via USB dongle (RTL8188EU tested) |
| **Bluetooth** | Via USB dongle |
| **Storage** | MicroSD (image ~1.2 GB, expands to full card) |
| **Video** | HDMI up to 1080p (adaptive) + Composite |
| **Kernel** | Linux 6.1.55 |

## Quick Start

### 1. Download

**[Download latest image](https://github.com/Yumi-Lab/Batocera-SmartPiOne/releases/latest)** (~1.1 GB)

### 2. Flash

Use [Balena Etcher](https://etcher.balena.io/), [Raspberry Pi Imager](https://www.raspberrypi.com/software/), or `dd`:

```bash
gunzip batocera-h3-smartpione-38-20231018.img.gz
sudo dd if=batocera-h3-smartpione-38-20231018.img of=/dev/sdX bs=1M status=progress
sync
```

### 3. Play

1. Insert SD card, connect HDMI and gamepad, power on
2. Batocera boots to EmulationStation (~60-90 seconds)
3. Configure WiFi from the ES menu
4. Add ROMs via network share (SMB) or USB

## Features

| Feature | Detail |
|---------|--------|
| **117 systems** | From Atari 2600 to PlayStation, arcade to home computers |
| **EmulationStation** | Frontend with scraper, themes, and per-game settings |
| **73 libretro cores** | + standalone emulators (Mupen64Plus, ScummVM) |
| **RetroAchievements** | Built-in — earn trophies on retro games |
| **Controllers** | Auto-detection USB & Bluetooth gamepads |
| **Network** | WiFi setup from ES menu + SMB file sharing for ROMs |
| **Updates** | Atomic — replace a single squashfs file |

## Emulation Performance

| Tier | Systems | Performance |
|------|---------|-------------|
| **Excellent** | NES, SNES, Game Boy, GBA, Mega Drive, Master System | Full speed |
| **Good** | PS1, Arcade (CPS1/CPS2/Neo-Geo), DOS, ScummVM | Most titles |
| **Limited** | N64, Dreamcast | Light titles only |
| **Not recommended** | PSP | Hardware limit |

> The H3 is comparable to a Raspberry Pi 2. For heavier systems, wait for **SmartPi 4** (H618 / Mali-G31 / Vulkan).

## Full List of Supported Systems (117)

| | | | |
|---|---|---|---|
| Abuse | Amiga 500 | Amiga 1200 | Amiga CD32 |
| Amiga CDTV | Amstrad CPC | Amstrad GX4000 | Apple II |
| Apple IIGS | Arduboy | Atari 2600 | Atari 5200 |
| Atari 7800 | Atari 800 | Atari Lynx | Atari ST |
| Atomiswave | Cannonball | Cave Story | C-Dogs SDL |
| Channel F | ColecoVision | Commodore 64 | Commodore 128 |
| Commodore PET | Commodore Plus/4 | Commodore VIC-20 | Commander Genius |
| Daphne | DevilutionX | DOS | Dreamcast |
| EasyRPG | Famicom Disk System | FinalBurn Neo | Flash |
| Game & Watch | Game Boy | Game Boy (2 Players) | Game Boy Advance |
| Game Boy Color | Game Boy Color (2P) | Game Gear | HCL |
| Hurrican | Intellivision | LowRes NX | Macintosh |
| MAME | Master System | Mega Drive | Mega Duck |
| Moonlight | Mr. Boom | MSU-MD | MSX |
| MSX2 | MSX2+ | MSX turboR | Multivision |
| Naomi | Neo-Geo | Neo-Geo CD | Neo-Geo Pocket |
| Neo-Geo Pocket Color | NES | Nintendo 64 | Nintendo 64DD |
| Odyssey² | OpenBOR | PC-88 | PC-98 |
| PC Engine | PC Engine CD | PICO-8 | Sega Pico |
| PlayStation | Pokémon Mini | Ports | PrBoom (Doom) |
| PSP | Quake III | SAM Coupé | Satellaview |
| ScummVM | SCV | SDLPoP (Prince of Persia) | Sega 32X |
| Sega CD | SG-1000 | Sharp X1 | Sharp X68000 |
| SNES | SNES MSU-1 | Solarus | Sonic Retro |
| Sufami Turbo | Super Bros War | Super Game Boy | SuperGrafx |
| Supervision | TheXTech | Thomson | TIC-80 |
| Tyrian | TyrQuake | Vectrex | Videopac+ |
| Virtual Boy | WonderSwan | WonderSwan Color | Xash3D FWGS (Half-Life) |
| XRick | ZC210 | ZX81 | ZX Spectrum |
| OD Commander | | | |

## What We Changed from Upstream Batocera

Only **board-level** additions — zero changes to emulators or Batocera core.

> **Note:** The current release (v38) uses the `orangepi-pc` board profile, which is fully compatible with SmartPi One H3. A dedicated `smartpi-one` board profile is prepared for a future build.

| File | Change |
|------|--------|
| `board/batocera/allwinner/h3/smartpi-one/` | New board: boot script, genimage, extlinux |
| `package/batocera/boot/uboot-multiboard/nanopi_m1/` | U-Boot DRAM tuning (576 MHz, ZQ=3881979, ODT) |
| `package/batocera/boot/uboot-multiboard/Config.in` | Added `nanopi_m1` to H3 U-Boot list |
| `package/batocera/core/batocera-system/Config.in` | Registered `smartpi-one` board |
| `configs/batocera-h3.board` | Added `sun8i-h3-nanopi-m1` DTB |
| `.github/workflows/build-smartpi-one.yml` | CI workflow |

<details>
<summary>Project structure</summary>

```
board/batocera/allwinner/h3/
├── smartpi-one/                    # SmartPi One board (NEW)
│   ├── boot/extlinux.conf          # Kernel boot config (nanopi-m1 DTB)
│   ├── create-boot-script.sh       # Image packaging script
│   └── genimage.cfg                # SD card layout (U-Boot nanopi_m1)
├── orangepi-pc/                    # (upstream) Reference H3 board
├── orangepi-one/                   # (upstream)
└── ...

package/batocera/boot/uboot-multiboard/
├── nanopi_m1/                      # SmartPi One DRAM config (NEW)
│   └── uboot.config.fragment       # CONFIG_DRAM_CLK=576, ZQ, ODT
├── common-h3/                      # (upstream) Shared H3 U-Boot config
└── Config.in                       # Board list (nanopi_m1 added)
```

</details>

## Build from Source

Requires a Linux x86_64 machine with **200 GB disk**, **8 GB RAM**, **4+ CPU cores**.
See [docs/BUILD-VM-SETUP.md](docs/BUILD-VM-SETUP.md) for Windows users (Ubuntu VM or WSL2).

```bash
git clone https://github.com/Yumi-Lab/Batocera-SmartPiOne.git
cd Batocera-SmartPiOne
make h3-build
```

| Phase | First build | Rebuild |
|-------|------------|---------|
| Toolchain | ~30 min | cached |
| Kernel + U-Boot | ~20 min | ~5 min |
| Packages (all emulators) | 3–6 h | ~1 h |
| Image generation | ~10 min | ~10 min |
| **Total** | **4–8 h** | **~1–2 h** |

<details>
<summary>Build requirements</summary>

| Resource | Minimum | Recommended |
|----------|---------|-------------|
| **OS** | Linux x86_64 (Ubuntu 22.04+) | Ubuntu 24.04 |
| **Disk** | 100 GB | 200 GB |
| **RAM** | 8 GB | 16 GB |
| **CPU** | 4 cores | 8+ cores |

</details>

## Roadmap

- [ ] **CPU frequency**: OPP table limited to 1008 MHz — add 1.2 GHz OPP in custom SmartPi One DTB (H3 supports up to 1.296 GHz)
- [ ] **Custom board profile**: Build with dedicated `smartpi-one` board instead of `orangepi-pc`
- [ ] **cpufreq driver**: Enable `CONFIG_CPU_FREQ` + `CONFIG_ARM_ALLWINNER_SUN50I_CPUFREQ_NVMEM` in kernel config for dynamic frequency scaling
- [ ] **Upgrade to Batocera v39/v40**

## Related Projects

| Project | Description |
|---------|-------------|
| [RetroMi](https://github.com/Yumi-Lab/RetroMi) | RetroPie + EmulationStation on Armbian for SmartPi One |
| [SmartPi-armbian](https://github.com/Yumi-Lab/SmartPi-armbian) | Armbian server base image |
| [SmartPi-BSP-kernel-linux](https://github.com/Yumi-Lab/SmartPi-BSP-kernel-linux) | Minimal BSP — bare Linux in 15 MB |
| [Batocera upstream](https://github.com/batocera-linux/batocera.linux) | Original Batocera project |

## Documentation

Full Batocera documentation: **[wiki.batocera.org](https://wiki.batocera.org/)**

Covers controls, scraping, netplay, themes, RetroAchievements, and more.

## License

MIT — Same as upstream Batocera.

---

<p align="center">
  <a href="https://batocera.org/"><strong>Batocera Linux</strong></a> ·
  <a href="https://www.yumi-lab.com"><strong>Yumi Lab</strong></a>
</p>
