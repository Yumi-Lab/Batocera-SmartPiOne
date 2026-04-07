# Build VM Setup — Windows + Ubuntu VM

## Pré-requis hardware
- **Disque** : 200 GB minimum alloués à la VM
- **RAM** : 8 GB minimum (16 GB recommandé)
- **CPU** : 4 cores minimum (8 recommandé — build parallèle)

## 1. Installer la VM Ubuntu

### Option A : VirtualBox (gratuit)
1. Télécharger VirtualBox : https://www.virtualbox.org/
2. Télécharger Ubuntu 24.04 Server : https://ubuntu.com/download/server
3. Créer la VM : 200 GB disque dynamique, 8 GB RAM, 4+ CPU
4. Installer Ubuntu Server (pas besoin du desktop)

### Option B : WSL2 (plus simple, pas de VM)
```powershell
wsl --install -d Ubuntu-24.04
```
Attention : WSL2 a une limite de disque par défaut à 256 GB, suffisant.

## 2. Installer les dépendances build

```bash
sudo apt-get update
sudo apt-get install -y \
  build-essential gcc g++ git wget cpio unzip rsync bc \
  libncurses5-dev python3 python3-setuptools swig \
  dosfstools mtools genimage libconfuse-dev \
  file bison flex libssl-dev device-tree-compiler \
  u-boot-tools lzop libmp3lame-dev python3-dev \
  libglib2.0-dev qt5-default libssl-dev || true
```

## 3. Cloner et builder

```bash
git clone https://github.com/Yumi-Lab/Batocera-SmartPiOne.git
cd Batocera-SmartPiOne
make h3-build
```

Premier build : **4-8h** selon la puissance CPU.
Rebuilds suivants : **1-2h** (cache Buildroot).

## 4. Résultat

```
output/h3/images/batocera/smartpi-one/batocera*.img
```

## 5. Flasher

Copier l'image vers Windows, puis flasher avec `dd` (pas Balena Etcher sur H3).

```bash
# Depuis la VM
scp output/h3/images/batocera/smartpi-one/batocera*.img user@windows-ip:/path/
```

## Temps de build estimés

| Phase | Premier build | Rebuild (cache) |
|-------|--------------|-----------------|
| **Toolchain** | ~30 min | skip |
| **Kernel + U-Boot** | ~20 min | ~5 min |
| **Packages (émulateurs)** | 3-6h | ~1h |
| **Image finale** | ~10 min | ~10 min |
