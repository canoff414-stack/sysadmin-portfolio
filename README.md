# Linux Homelab

A running log of my Linux system administration practice — labs, scripts, and notes from a self-directed 90-day study plan working toward RHCSA (EX200) and IT support / cloud sysadmin roles.

## Background

I hold CompTIA Security+ (DoD 8140 IAT Level II) and I'm building hands-on Linux administration skills to pair with it — storage/LVM, networking, SELinux, systemd, scripting, containers (Podman), security hardening, and basic cloud deployment.

## Labs

Each week has up to two files in `labs/`: the polished capstone write-up (goal, setup, verification, what I learned) and a daily exercise checklist for the drills leading up to it.

| Week | Capstone Lab | Daily Exercises | Topics |
|------|-------------|------------------|--------|
| 1 | [Team Directory Permissions & SGID](labs/week01-permissions-sgid.md) | — | chmod, sticky bit, SGID |
| 2 | [Sudo Privilege Levels & Dual Package Management](labs/week02-users-sudo-packages.md) | [Exercises](labs/week02-exercises.md) | sudo, sudoers, dnf, apt, Podman |

*(This table grows as each week is added — `labs/TEMPLATE.md` for the capstone format, `labs/EXERCISES_TEMPLATE.md` for the daily checklist.)*

## Weekly convention

Starting Week 2, every week adds two files to `labs/`:

- `weekNN-<topic-slug>.md` — the Day 6 capstone, copied from `TEMPLATE.md`
- `weekNN-exercises.md` — the Day 1–5 daily drills, copied from `EXERCISES_TEMPLATE.md`

Both get added to the table above when they're pushed.

## Scripts

Standalone scripts live in [`scripts/`](scripts/), each referenced from the lab writeup that produced it.

## Structure

```
linux-homelab/
├── README.md
├── labs/
│   ├── TEMPLATE.md
│   ├── EXERCISES_TEMPLATE.md
│   ├── week01-permissions-sgid.md
│   ├── week02-users-sudo-packages.md
│   └── week02-exercises.md
└── scripts/
```
