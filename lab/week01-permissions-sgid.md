# Lab: Team Directory Permissions & SGID

**Goal:** Set up shared project directories where two teams have private
workspaces plus a shared drop folder, without permission leakage between
groups.

## Setup

```bash
sudo groupadd engteam
sudo groupadd projmanteam
sudo useradd -m -G engteam eng1
sudo useradd -m -G projmanteam projman1
sudo mkdir -p /srv/project/{eng,projman,shared}
```

## What I did

- Set `770` on the team-private folders (`eng`, `projman`) so only the owner
  (root) and the team's group have any access at all — everyone else gets
  nothing.
- Set `1777` on the shared folder so anyone can create files
  there, but only a file's own owner (or root) can delete or rename it —
  the same protection `/tmp` uses.
- Set `2770` (SGID) on the dev folder so new files automatically inherit
  the `engteam group instead of the creating user's own default group.
  Without this, every file `eng1` creates would default to a personal
  `eng1` group, and other team members would lose access to it.

```bash
sudo chown root:engteam /srv/project/eng
sudo chmod 2770 /srv/project/eng

sudo chown root:projmanteam /srv/project/projman
sudo chmod 770 /srv/project/projman

sudo chown root:root /srv/project/shared
sudo chmod 1777 /srv/project/shared
```

## Verification

```
$ ls -ld /srv/project/eng
drwxrws--- 2 root devteam 4096 Sep 22 10:03 /srv/project/eng

$ ls -ld /srv/project/projman
drwxrws--- 2 root projmanteam  4096 Sep 22 10:03 /srv/project/projman

$ ls -ld /srv/project/shared
drwxrwxrwt 2 root root    4096 Sep 22 10:03 /srv/project/shared
```

## What I learned

SGID on a directory solves a real coordination problem: without it, file
ownership drifts to whoever happened to create each file, and teammates
silently lose access over time. The lowercase `s` in the group execute
position of `drwxrws---` confirms SGID is active with execute also set
an uppercase `S` would mean SGID was set but group execute was off, which
is a common gotcha worth recognizing on sight. The sticky bit solves a
different problem (preventing deletion in a shared writable space) and the
two are easy to confuse until you've used both side by side like this.
