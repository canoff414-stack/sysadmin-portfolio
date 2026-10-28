# Week 2 Exercises — Users, Groups & Package Management

Daily drills, tracked here as I complete them. The Day 6 capstone lab is
written up separately in
[week02-users-sudo-packages.md](week02-users-sudo-packages.md).

## Day 1 — User & Group Fundamentals

- [ ] Create `test1` with a home directory; confirm `/home/test1` exists
- [ ] Create group `auditors`, add `test1` as a secondary member; verify
      with `id` and `groups`
- [ ] Lock `test1` with `passwd -l`; inspect the changed hash field in
      `/etc/shadow`
- [ ] Walk through all seven colon-separated fields of a `/etc/passwd`
      line for `root` and my own user
- [ ] Delete `test1` including its home directory; confirm removal

## Day 2 — sudo & /etc/sudoers

- [ ] Add a user to `wheel`; confirm with `sudo -l`
- [ ] Write a `visudo` rule limiting a second user to one specific
      command, no password required
- [ ] Confirm the allowed command works and a disallowed one is denied
- [ ] Confirm `sudo -l` output matches the sudoers line exactly
- [ ] Compare `su - user` vs `sudo -u user whoami` in my own words

## Day 3 — dnf & rpm

- [ ] `dnf search` then `dnf info` before installing a package
- [ ] Install a package, list its files with `rpm -ql`
- [ ] Reverse-lookup a file to its package with `rpm -qf`
- [ ] Undo an install via `dnf history undo`
- [ ] Compare `rpm -qf` results for an rpm-owned file vs. one that isn't

## Day 4 — apt & dpkg

- [ ] Spin up a disposable Ubuntu shell with
      `podman run -it --rm ubuntu bash`
- [ ] Install a package, inspect it with `dpkg -s` and `dpkg -L`
- [ ] Compare `apt remove` vs. `apt purge` on a package with a config file
- [ ] Confirm the container is fully disposable after `exit`

## Day 5 — Process Management

- [ ] Background a `sleep` job; find its PID with `ps aux`
- [ ] Practice `fg` / `Ctrl+Z` / `bg` on that job
- [ ] Kill it by PID; confirm it's gone
- [ ] Watch a process live in `top`, note its NI value
- [ ] `renice` a running process; confirm the change in `top`
