# ✅ BlackArch Tools Installation

---

## Categories Installed

```bash
sudo pacman -S blackarch-forensic
sudo pacman -S blackarch-recon
sudo pacman -S blackarch-exploitation
sudo pacman -S blackarch-fuzzer
```

---

## Forensics — `blackarch-forensic`
Tools: `autopsy`, `volatility3`, `binwalk`, `foremost`, `sleuthkit`, `dc3dd`, `guymager`, `trid`, `unblob`

**Use case:** Analyzing honeypot-captured artifacts — disk images, memory dumps, malicious files.

---

## Reconnaissance — `blackarch-recon`
Tools: `nmap`, `masscan`, `gobuster`, `nikto`, `whatweb`, `sherlock`

**Use case:** Scanning the honeypot from the attacker's perspective.

---

## Exploitation — `blackarch-exploitation`
Tools: `sqlmap`, `hydra`, `john`, `hashcat`, `exploitdb`

**Note:** `metasploit` unavailable on ARM64 (requires `wine`, `mingw-w64-gcc`).

**Use case:** Testing attack vectors against the honeypot's fake SSH/HTTP services.

---

## Fuzzing — `blackarch-fuzzer`
Tools: `ffuf`, `wfuzz`, `burpsuite`, `radamsa`

**Use case:** Fuzzing honeypot HTTP endpoints to find detection gaps.

---

## Dependency Choices During Install

| Dependency | Choice | Reason |
|---|---|---|
| `java-environment` | `jdk17-openjdk` (3) | Most stable |
| `jack` | `pipewire-jack` (2) | Modern backend |
| `oci-runtime` | `crun` (1) | Lightweight |
| `qt6-python` | `python-pyqt6` (2) | Standard |
| `ttf-font` | `noto-fonts` (2) | Best coverage |

---

## Expected ARM64 Warnings (Normal)

These are not errors — just packages unavailable on aarch64:
- `metasploit`, `wine`, `mingw-w64-gcc`, `responder`
![Image of tool installation](screenshots/
