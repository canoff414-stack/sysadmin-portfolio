# Linux Homelab

A running log of my Linux system administration practice — labs, scripts, and notes from a self-directed 90-day study plan working toward RHCSA (EX200) and IT support / cloud sysadmin roles.

## Background

I hold CompTIA Security+ (DoD 8140 IAT Level II) and I'm building hands-on Linux administration skills to pair with IT storage/LVM, networking, SELinux, systemd, scripting, containers (Podman), security hardening, and basic cloud deployment.

## Labs

| Week | Lab | Topics |
|------|-----|--------|
| 1 | [Team Directory Permissions & SGID](labs/week01-permissions-sgid.md) | chmod, sticky bit, SGID |

*(This table grows as each lab is added — see `labs/TEMPLATE.md` for the format used.)

## Scripts

Standalone scripts live in [`scripts/`](scripts/), each referenced from the lab writeup that produced it.

## Structure

```
linux-homelab/
├── README.md
├── labs/
│   ├── TEMPLATE.md
│   └── week01-permissions-sgid.md
└── scripts/
```
