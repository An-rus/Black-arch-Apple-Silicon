# BlackArch Linux — ARM64 Security Research Environment

> A systematic documentation of deploying a BlackArch Linux penetration testing environment on Apple Silicon (M2) using containerized virtualization. This repository records the full experimental process, including failed methodologies and their root cause analysis.

---

## Abstract

This project establishes a reproducible BlackArch Linux security research environment on an ARM64 host (Apple Silicon M2). The primary challenge addressed is the architectural incompatibility between x86_64-centric security tooling and the aarch64 instruction set, compounded by hypervisor-level networking constraints inherent to QEMU-based virtualization on macOS.

The final architecture leverages OrbStack's native ARM64 containerization as a superior alternative to traditional VM approaches, achieving full BlackArch repository integration with forensic, reconnaissance, exploitation, and fuzzing toolsets.

---

## System Specifications

| Component | Specification |
|---|---|
| Host Architecture | ARM64 (Apple Silicon M2) |
| Host OS | macOS |
| Virtualization Layer | OrbStack (native ARM64 containers) |
| Guest Architecture | aarch64 |
| Guest OS | Arch Linux (latest) |
| Security Overlay | BlackArch Linux repository |
| Kernel | Linux aarch64 (ALARM) |

---

## Research Objectives

1. Deploy a functional BlackArch environment on ARM64 hardware
2. Document architectural constraints and incompatibilities
3. Establish a reproducible methodology for Apple Silicon security workstations
4. Build a controlled lab environment for honeypot defense research

---

## Methodology

### Experimental Approach

Each virtualization method was tested systematically. Failures were documented with root cause analysis before proceeding to the next approach. This iterative methodology produced a complete compatibility matrix for ARM64 Linux deployment on macOS.

### Compatibility Matrix

| Method | Network | Tools | BlackArch | Result |
|---|---|---|---|---|
| UTM + Arch ISO (aarch64) | ✅ | ❌ | ❌ | ❌ Discarded |
| UTM + Archboot | ❌ | ✅ | — | ❌ Discarded |
| UTM + Debian bridge | ❌ | ✅ | — | ❌ Discarded |
| UTM Gallery images | ❌ | ✅ | ❌ | ❌ Discarded |
| OrbStack (Arch) | ✅ | ✅ | ✅ | ✅ **Selected** |

---

## Repository Structure

```
Black-arch-and-configuration/
├── README.md
├── 01-instalacion/
│   ├── intentos-fallidos.md    ← Failed methodologies + RCA
│   └── orbstack-setup.md       ← Validated deployment procedure
├── 02-blackarch/
│   └── blackarch-repo.md       ← Repository integration + errors
├── 03-herramientas/
│   └── instalacion.md          ← Toolset deployment by category
├── 04-gui/
│   └── intentos-fallidos.md    ← X11 forwarding investigation
└── screenshots/                ← Empirical evidence per step
```

---

## Results

### Successfully Deployed Toolsets

| Category | Package | Primary Use Case |
|---|---|---|
| Digital Forensics | `blackarch-forensic` | Artifact analysis from honeypot captures |
| Reconnaissance | `blackarch-recon` | Attack surface mapping |
| Exploitation | `blackarch-exploitation` | Vulnerability validation |
| Fuzzing | `blackarch-fuzzer` | Input boundary testing |

### Known ARM64 Limitations

The following tools are unavailable on aarch64 due to hard x86_64 dependencies:

- `metasploit` — requires `wine` and `mingw-w64-gcc`
- `responder` — requires `mingw-w64-gcc`
- Several PyQt4/Qt5 bindings — deprecated or x86-only builds

These limitations are architectural constraints of the aarch64 platform, not configuration errors.

---

## Progress

- [x] Hypervisor compatibility research
- [x] ❌ UTM + Arch ISO — insufficient tooling in image
- [x] ❌ UTM + Archboot — VirtIO network initialization failure
- [x] ❌ UTM + Debian bridge — same DHCP failure, different distro
- [x] ❌ UTM Gallery — incompatible with BlackArch overlay
- [x] ✅ OrbStack deployment — validated
- [x] ✅ BlackArch repository — manual integration
- [x] ✅ Forensic toolset — deployed
- [x] ✅ Reconnaissance toolset — deployed
- [x] ✅ Exploitation toolset — deployed
- [x] ✅ Fuzzing toolset — deployed
- [ ] Graphical environment (Hyprland/Wayland) — future work

---

## Application Domain

This environment is designed for controlled security research, specifically:

- **Honeypot defense testing** — attacking a self-hosted honeypot to identify detection gaps
- **Digital forensics** — analyzing captured attack artifacts
- **Vulnerability research** — controlled exploitation in isolated lab conditions

All testing is conducted exclusively on self-owned infrastructure. Unauthorized use of these tools against external systems is illegal and outside the scope of this project.

---

## References

- [BlackArch Linux](https://blackarch.org) — Security research distribution
- [OrbStack](https://orbstack.dev) — ARM64-native Linux containers for macOS
- [Arch Linux ARM](https://archlinuxarm.org) — Arch Linux for ARM architectures
