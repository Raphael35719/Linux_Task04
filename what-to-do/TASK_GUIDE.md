# Task Guide — Linux Practical Test Package

This guide follows the 10 activities in the supplied Task 04 PDF.

## Activity 1 — Navigation & File Management
```bash
mkdir -p linux_lab/docs linux_lab/scripts
cd linux_lab
touch notes.txt script.sh
echo "Welcome to Linux Practice" > readme.txt
cp readme.txt docs/
mv notes.txt docs/
rm script.sh
tree .
# or: ls -R
```

## Activity 2 — File Viewing & Editing
Open `readme.txt`, add your name at the bottom, and write the functions of Kernel, FHS, and Shell:
```bash
nano readme.txt
head -n 3 readme.txt
tail -n 2 readme.txt
wc readme.txt
grep "Linux" readme.txt
```
- **Kernel:** manages hardware and system resources and provides core operating-system services.
- **FHS (Filesystem Hierarchy Standard):** defines the standard Linux directory layout.
- **Shell:** provides a command interface between the user and operating system.

## Activity 3 — Permissions & Ownership
```bash
touch secure.txt
chmod 640 secure.txt
ls -l secure.txt
chmod 777 secure.txt
ls -l secure.txt
```
Mode `640` means owner read/write, group read-only, others no access. The worksheet then asks for `777`, which grants read/write/execute to everyone; use this only in your lab. If permitted, create `student2` and change ownership:
```bash
sudo useradd -m -s /bin/bash student2
sudo chown student2 secure.txt
ls -l secure.txt
```
If `student2` already exists, inspect it instead of creating a duplicate.

## Activity 4 — Archiving & Compression
```bash
mkdir -p backup_test
printf "File one\n" > backup_test/file1.txt
printf "File two\n" > backup_test/file2.txt
printf "File three\n" > backup_test/file3.txt
tar -cvf backup.tar backup_test
gzip -c backup.tar > backup.tar.gz
mkdir -p restore_test
tar -xvzf backup.tar.gz -C restore_test
find restore_test -type f
```
Verify all three files were restored under `restore_test/backup_test/`.

## Activity 5 — Process Management
```bash
sleep 300 &
jobs
fg
```
When the process is in the foreground, press `Ctrl+C` to stop it. Check for any remaining matching process:
```bash
pgrep -a sleep
ps aux | grep '[s]leep'
```
If a `sleep 300` process remains, terminate only that process using its actual PID:
```bash
kill PID
```
Replace `PID` with the real process ID. Verify it stopped, then run `top` and press `q` to exit. Do not terminate unrelated processes.

## Activity 6 — Networking Basics
```bash
ip a
ping google.com -c 4
ss -tulnp
hostname
```
Edit hosts file:
```bash
sudo nano /etc/hosts
```
Add the following line if it is not already present:
```text
127.0.0.1 testsite.local
```
Save, then verify:
```bash
getent hosts testsite.local
ping testsite.local -c 4
```
This maps the name to the local loopback address; it does not create a public website. Internet connectivity depends on network/DNS availability.

## Activity 7 — Searching & Finding
```bash
find / -name readme.txt 2>/dev/null
grep -R "Linux" --include="*.txt" docs/
find ~ -type f -mmin -1440
find ~ -type f -name "*.txt" | wc -l
```

## Activity 8 — Package Management (Debian/Ubuntu-based)
```bash
sudo apt update
sudo apt install tree
tree --version
sudo apt remove tree
dpkg -l > packages.txt
```
The worksheet asks you to remove `tree`, so capture its version before removing it.

## Activity 9 — Scripting Basics
Create `hello.sh`:
```bash
cat > hello.sh <<'EOF'
#!/usr/bin/env bash
echo "Hello, Linux World!"
date
pwd
EOF
chmod +x hello.sh
./hello.sh
```

## Activity 10 — System Monitoring & Logs
```bash
df -h
free -h
sudo tail -n 10 /var/log/syslog
```
If `/var/log/syslog` is unavailable, try `/var/log/messages`. If neither exists, use:
```bash
sudo journalctl -n 10
```
Then:
```bash
uptime
who
lscpu
```

## Final verification
Verify the files, permissions, archive and restored contents, process termination, local host entry, package list, script output, and system information. Save genuine screenshots and outputs in `evidence/` and `outputs/`.
