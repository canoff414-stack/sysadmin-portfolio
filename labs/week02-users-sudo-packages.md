# Lab: Sudo Privilege Levels & Dual Package Management

**Goal:** Set up three users representing three common real-world access
levels — full admin, limited admin (one specific task only), and no
elevated access — then verify each boundary. Then confirm package
management competency on both RHEL-family and Debian-family systems.

## Setup

```bash
sudo useradd -m admin1
sudo useradd -m helpdesk1
sudo useradd -m readonly1
sudo passwd admin1
sudo passwd helpdesk1
sudo passwd readonly1
```

## What I did

**Full admin via the wheel group**

```bash
sudo usermod -aG wheel admin1
```

Verified by switching to `admin1` and running `sudo dnf update` — it
prompted for `admin1`'s password and succeeded.

**Limited admin — can only restart one service, nothing else**

A help desk tech often needs to restart a specific service without
broader root access. Added this line via `visudo`:

```
helpdesk1 ALL=(root) NOPASSWD: /usr/bin/systemctl restart httpd
```

Verified `helpdesk1` could run exactly that command with no password
prompt, and was denied for anything else (`sudo dnf install tree` was
refused).

**No elevated access — baseline comparison**

`readonly1` got no sudoers entry at all, confirming the default-deny
baseline actually holds (`sudo whoami` was refused with the standard "is
not in the sudoers file" message).

**Package management — dnf side**

```bash
sudo dnf install tree -y
tree --version
sudo dnf remove tree -y
rpm -qa | grep tree     # returned nothing, confirming removal
```

**Package management — apt side**

Used a disposable Ubuntu container via Podman instead of a second VM:

```bash
podman run -it --rm ubuntu bash
```

Inside that shell:

```bash
apt update
apt install tree -y
tree --version
apt remove tree -y
dpkg -l | grep tree     # returned nothing
exit
```

## Verification

```
$ groups admin1
admin1 : admin1 wheel

$ sudo cat /etc/sudoers | tail -1
helpdesk1 ALL=(root) NOPASSWD: /usr/bin/systemctl restart httpd

$ su - readonly1 -c "sudo whoami"
readonly1 is not in the sudoers file. This incident will be reported.
```

## What I learned

The real lesson here is least privilege as a practice, not just a
sudoers syntax exercise: `admin1` can do anything, `helpdesk1` can do
exactly one administrative task and nothing else, and `readonly1` proves
the default-deny baseline actually holds. In a real environment this is
the difference between a help desk tier that can fix the one thing
they're trained on versus a security incident waiting to happen from
over-provisioned access. On the package side, being able to move between
`dnf` and `apt` without hesitation matters because job postings rarely
specify which distro family you'll actually touch day to day, and the
Podman one-liner meant I didn't need a second VM just to practice apt.
