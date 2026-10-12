# Command Reference

### Files and text
```bash
mkdir -p linux_lab/docs linux_lab/scripts
echo "Welcome to Linux Practice" > readme.txt
cp readme.txt docs/
mv notes.txt docs/
rm script.sh
head -n 3 readme.txt
tail -n 2 readme.txt
wc readme.txt
grep "Linux" readme.txt
```

### Permissions, archive, process
```bash
chmod 640 secure.txt
chmod 777 secure.txt
sudo chown student2 secure.txt
tar -cvf backup.tar backup_test
gzip -c backup.tar > backup.tar.gz
tar -xvzf backup.tar.gz -C restore_test
sleep 300 &
jobs
pgrep -a sleep
top
```

### Search, networking, packages, monitoring
```bash
find / -name readme.txt 2>/dev/null
grep -R "Linux" --include="*.txt" docs/
ip a
ping google.com -c 4
ss -tulnp
hostname
getent hosts testsite.local
sudo apt update
sudo apt install tree
tree --version
sudo apt remove tree
dpkg -l > packages.txt
df -h
free -h
uptime
who
lscpu
```
