# ✅ BlackArch Repository Setup

---

## ❌ Method 1 — Official Script (Partially failed)

```bash
curl -O https://blackarch.org/strap.sh
chmod +x strap.sh
sudo ./strap.sh
```

Script ran and showed `BlackArch repository is ready!` but wrote `include` (lowercase) in pacman.conf instead of `Include`. Pacman ignores lowercase directives silently.

**Error:** `directive 'include' not recognized`

---

## ✅ Method 2 — Manual Setup

### 1. Create mirrorlist
```bash
sudo tee /etc/pacman.d/blackarch-mirrorlist << 'EOF2'
Server = https://blackarch.org/blackarch/$repo/os/$arch
EOF2
```

### 2. Add to pacman.conf
```bash
sudo nano /etc/pacman.conf
# Add at end — capital I in Include is required:
[blackarch]
Include = /etc/pacman.d/blackarch-mirrorlist
```

### 3. Fix SigLevel (ARM64 key trust issue)
```bash
# In pacman.conf, change:
SigLevel = Required DatabaseOptional
# To:
SigLevel = Optional TrustAll
```

### 4. Import keys
```bash
sudo pacman-key --init
sudo pacman-key --recv-keys 4345771566D76038C7FEB43863EC0ADBEA87E4E3
sudo pacman-key --lsign-key 4345771566D76038C7FEB43863EC0ADBEA87E4E3
```

### 5. Sync
```bash
sudo pacman -Syy
# Should show: core, extra, alarm, aur, blackarch
```
