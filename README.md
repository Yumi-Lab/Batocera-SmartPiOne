# Batocera-SmartPiOne

[Batocera Linux](https://batocera.org/) port for the [SmartPi One](https://www.yumi-lab.com) (Allwinner H3) by Yumi Lab.

Turn your SmartPi One into a plug-and-play retrogaming console with 50+ emulators, scraper, RetroAchievements, and a polished UI — powered by the Batocera community.

> This is a fork of [batocera-linux/batocera.linux](https://github.com/batocera-linux/batocera.linux) with SmartPi One board support added.

## SmartPi One hardware

| Spec | Detail |
|------|--------|
| **SoC** | Allwinner H3 — Cortex-A7 quad-core @ 1.2 GHz |
| **RAM** | 1 GB DDR3 (576 MHz, custom tuning) |
| **GPU** | Mali-400 MP2 — Lima (GLES 2.0) |
| **WiFi** | RTL8188EU (on-board) |
| **Storage** | MicroSD |
| **Video** | HDMI 1080p + Composite |

## What you get

| Feature | Detail |
|---------|--------|
| **Emulators** | 50+ systems — NES, SNES, Mega Drive, PS1, GBA, N64, arcade, and more |
| **Frontend** | Batocera EmulationStation (themes, scraping, per-game settings) |
| **GPU driver** | Lima (open-source Mesa, GLES 2.0) |
| **RetroAchievements** | Built-in support |
| **Controllers** | Auto-detection USB/BT gamepads |
| **Network** | WiFi config from ES menu |
| **Updates** | Atomic update (replace single squashfs file) |
| **Boot time** | ~60-90 seconds to EmulationStation |

### Emulation performance (H3 reality check)

| System | Performance |
|--------|------------|
| NES / SNES / Game Boy / GBA | Excellent |
| Mega Drive / Master System | Excellent |
| PS1 (easy titles) | Good |
| N64 | Poor (hardware limit) |
| PSP | Not recommended |
| Arcade (CPS1/CPS2/Neo-Geo) | Good to Excellent |
| DOS / ScummVM | Good |

The H3 is comparable to a Raspberry Pi 2 in emulation capability. For heavier systems, wait for SmartPi 4 (H618/Mali-G31/Vulkan).

## What we changed from upstream Batocera

Only **board-level** additions — zero changes to emulators or Batocera core.

> **Note:** The current release image (v38) uses the `orangepi-pc` board profile, which is fully compatible with the SmartPi One H3. The custom `smartpi-one` board profile below is prepared for a future build.

| File | Change |
|------|--------|
| `board/batocera/allwinner/h3/smartpi-one/` | New board: boot script, genimage, extlinux |
| `package/batocera/boot/uboot-multiboard/nanopi_m1/` | U-Boot DRAM tuning (576MHz, ZQ=3881979, ODT) |
| `package/batocera/boot/uboot-multiboard/Config.in` | Added `nanopi_m1` to H3 U-Boot list |
| `package/batocera/core/batocera-system/Config.in` | Registered `smartpi-one` board |
| `configs/batocera-h3.board` | Added `sun8i-h3-nanopi-m1` DTB |
| `.github/workflows/build-smartpi-one.yml` | CI workflow |

## Quick start

### Download

Pre-built images available in [Releases](https://github.com/Yumi-Lab/Batocera-SmartPiOne/releases) (when available) or as [GitHub Actions artifacts](https://github.com/Yumi-Lab/Batocera-SmartPiOne/actions).

### Flash

Use [Balena Etcher](https://etcher.balena.io/), [Raspberry Pi Imager](https://www.raspberrypi.com/software/), or `dd`:

```bash
gunzip batocera-smartpi-one.img.gz
sudo dd if=batocera-smartpi-one.img of=/dev/sdX bs=1M status=progress
sync
```

### First boot

1. Insert SD card, connect HDMI and gamepad, power on
2. Batocera boots directly to EmulationStation
3. Configure WiFi from the ES menu
4. Add ROMs via network share (SMB) or USB

## Build from source

Requires a Linux x86_64 machine with **200 GB disk**, **8 GB RAM**, **4+ CPU cores**.
See [docs/BUILD-VM-SETUP.md](docs/BUILD-VM-SETUP.md) for Windows users (Ubuntu VM or WSL2).

```bash
git clone https://github.com/Yumi-Lab/Batocera-SmartPiOne.git
cd Batocera-SmartPiOne
make h3-build
```

| Phase | First build | Rebuild (cache) |
|-------|------------|-----------------|
| **Toolchain** | ~30 min | cached |
| **Kernel + U-Boot** | ~20 min | ~5 min |
| **Packages (all emulators)** | 3-6h | ~1h |
| **Image generation** | ~10 min | ~10 min |
| **Total** | **4-8h** | **~1-2h** |

Output: `output/h3/images/batocera/smartpi-one/batocera*.img`

## Build requirements

| Resource | Minimum | Recommended |
|----------|---------|-------------|
| **OS** | Linux x86_64 (Ubuntu 22.04+) | Ubuntu 24.04 |
| **Disk** | 100 GB | 200 GB |
| **RAM** | 8 GB | 16 GB |
| **CPU** | 4 cores | 8+ cores |
| **Time** | 8 hours | 4 hours |

## Project structure (SmartPi additions)

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

## Related projects

| Project | Description |
|---------|-------------|
| [RetroMi](https://github.com/Yumi-Lab/RetroMi) | Custom retrogaming image (RetroPie + EmulationStation on Armbian) |
| [SmartPi-BSP-kernel-linux](https://github.com/Yumi-Lab/SmartPi-BSP-kernel-linux) | Minimal BSP — bare Linux in 15 MB, boots in 5 seconds |
| [SmartPi-armbian](https://github.com/Yumi-Lab/SmartPi-armbian) | Armbian server base image |
| [Batocera upstream](https://github.com/batocera-linux/batocera.linux) | Original Batocera project |

## Documentation

Full Batocera documentation (controls, scraping, netplay, themes, etc.):
**[wiki.batocera.org](https://wiki.batocera.org/)**

## Credits

- [Batocera Linux](https://batocera.org/) — the amazing retrogaming distribution
- [Yumi Lab](https://www.yumi-lab.com) — SmartPi One hardware and board support

## License

MIT — Same as upstream Batocera.
