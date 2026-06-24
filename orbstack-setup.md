# ✅ OrbStack Setup — Arch Linux ARM64

---

## Why OrbStack

| Feature | UTM | OrbStack |
|---|---|---|
| Network | ❌ DHCP issues on M2 | ✅ Works automatically |
| ARM64 | ✅ | ✅ Native |
| Setup | Complex | ✅ One command |

---

## Setup

1. Download OrbStack from [orbstack.dev](https://orbstack.dev)
2. Open OrbStack → Machines → `+`

```
Name:         BlackArch
Distribution: Arch
Version:      Latest
Architecture: arm64
```

---

## Verification

```bash
uname -m          # aarch64
ping -c 3 google.com   # 0% packet loss
sudo pacman -Syu
```
