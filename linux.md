### apt
```shell
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 40976EAF437D05B5
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32

apt-get update && apt-get install -y git vim

apt-get install -t wheezy-backports nginx

/etc/apt/sources.list.d/
```

### arp
```shell
-na
```

### awk
```shell
[inserting a new column called 'ndx' starting at count 0 and incrementing]
awk 'BEGIN{ndx=0}{print ndx, $1, $8; ndx+=1}’

awk -Wversion 2>/dev/null || awk --version
```

### chkconfig (service) (see also systemctl)
```shell
-—list
--level 2345 appd4db off
--list appd4db
  appd4db            0:off    1:off    2:off    3:off    4:off    5:off    6:off
```

### chmod
```shell
g+s [inherit the group ID on any new files or subdirectories created]
a+r [grant read perms to everyone]

+ == <add perms>
- == <rm perms>
= == <the only perms the file has>

u == <user who owns it>
g == <group owner>
o == <other users not in group>
a == <all users>

rwx == <duh>
X == <execute only if directory>
s == <set user or group ID>
```   
   
### curl
```shell
-d “@filename.foo”
-u “user"
-w “%{http_code} %{time_total}”
-x <proxy>
-X GET|POST
-O (download file)
-H "Authorization: bearer ${access_token}”
```

### cut
```shell
-f<field number> (no space)
-d<field separator> (no space)

cut -f2 -d” "
```    

### dd
```shell
dd if=/dev/zero of=/db/oracle/data/output conv=fdatasync bs=384k count=5k; rm -f /db/oracle/data/output
```

### dmesg
```shell

```

### docker
```shell
run [runs the container]
-t [assigns a pseudo-tty inside the container]
-i [makes an interactive connection to SDTIN of the container]
-d [daemonizes the container]
-c [run command]

run [image:version] -t -i /bin/bash

run -d ubuntu:14.04 /bin/sh -c "while true; do echo hello world; sleep 1; done"

logs [container name or id]

logs 1b24f82b469b

images [lists all images on local machine]

pull <image_name>
```

### dpkg (debian & variants)
```shell
--get-selections [show installed packages]

filesystems (mount -t <type>)
/etc/filesystems

note: cifs will show up after a drive is mounted 
mount -t cifs //host/share /mnt/share
```

### find
```shell
-ctime +n (n*24)
-size +n[G|M|k|b]
-exec <command> '{}'  \;
| xargs <command>

Find files on / (root) only:
find / -xdev -type f -size +100M -exec ls -la {} \;
```

### fstab
```shell
to mount a cifs share at boot:
//<hostname>/bsm_offline /mnt/offline cifs rw,noexec,credentials=/etc/fstab_cifs_account 0 0
  credentials file:
     username=[<domain>/]<user>
     password=<passwd>
```

### grep
```shell
-o Print only the matched (non-empty) parts of a matching line, with each such part on a separate output line.

-E egrep functionality. preferred over egrep
```

### i2cdetect
```shell
see ‘raspberry pi page'
```

### i2cget
```shell
see ‘raspberry pi page'
```

### i2cset
```shell
see ‘raspberry pi page'
```

### IFS
```shell
IFS=$'\n’
```

### inodes
```shell
Find the dir using the most inodes
for i in /app/ada/NTCdb/oracle/*; do echo $i; find $i |wc -l | sort ; done
```

### ipset
```shell
add add 10.0.0.0/20
del ronin 10.0.0.0/20
list <setname>
list ronin
```

### iptables
```shell
—list or service iptables status
iptables-restore < <rules_file>
```

### iwconfig  (configure a wireless network interface)

### iwlist
```shell
sudo iwlist wlan0 scan
```

### jar
```shell
to list the table of contents of a jar file
jar tf webapps/ROOT/WEB-INF/lib/catalina-root.jar

to extract the contents
jar xf file.jar

to extract a specific file
jar xf sample.war WEB-INF/web.xml

to archive two class files into an archive called classes.jar:
jar cvf classes.jar Foo.class Bar.class
    
to create a WAR:    
jar -cvf myServletWAR.war .
```

### jmxterm
```shell
/app/platform/java/current/bin/java -jar /var/tmp/jmxterm-1.0-alpha-4-uber.jar

$>domains
#following domains are available
JMImplementation
com.sun.management
java.lang
java.nio
java.util.logging
log4j
org.apache.ZooKeeperService

$>domain java.lang
#domain is set to java.lang

$>beans
#domain = java.lang:
java.lang:name=Code Cache,type=MemoryPool
java.lang:name=CodeCacheManager,type=MemoryManager
...
java.lang:type=OperatingSystem
java.lang:type=Runtime
java.lang:type=Threading

$>bean java.lang:type=OperatingSystem
#bean is set to java.lang:type=OperatingSystem

$>info
#mbean = java.lang:type=OperatingSystem
#class name = sun.management.OperatingSystemImpl
# attributes
  %0   - Arch (java.lang.String, r)
  ...
  %8   - OpenFileDescriptorCount (long, r)
  ...
  %15  - Version (java.lang.String, r)
#there's no operations
#there's no notifications

$>get OpenFileDescriptorCount
#mbean = java.lang:type=OperatingSystem:
OpenFileDescriptorCount = 99;

$ java -jar jmxterm-1.0-alpha-4-uber.jar -v silent -n < jmxcommands 
```

### jq
```shell
see jq page

- curl https://api.g4.app.cloud.net/v2/apps/dcc568a8-c9ba-4d68-a00b-123cd09d9c38/env -H "Authorization: bearer ${token}" | jq '.[].VCAP_SERVICES’
- | jq '.[].VCAP_APPLICATION.limits.mem'

If name has special chars such as “-“

- | jq '.[].VCAP_SERVICES."p-rabbitmq”'
```

### lsblk
```shell
--nodeps
--noheadings
-o KNAME,TYPE,MODEL
```

### lsof

### lspci
```shell
show HW/bus/video/eNet/etc
lspci -v
```

### lsusb

### mail
```shell
echo -e "difference found in $conf" '\n' "see `hostname`:$LOG" '\n' | /bin/mail -s "RUM Filters" foo@bar.com
```

### mount
```shell
mount -t iso9660 -o loop <iso> <mount>
```

### msiexec.exe
```shell
/package package.msi
/quiet
/l* output.log
```

### nc (netcat)
```shell
nc -w20 -vv vax 1984 (conn to remotehost (vax) on port 1984, very verbose, drop conn after 20 secs)
```

### nohup
```shell
nohup <command> > /dev/null 2>&1 & # runs in background, still doesn't create nohup.out
```

### od

### profile.d
```shell
for RHEL create /etc/profile.d/<name>.sh
Use export <var>=<value>
```

### ps
```shell
-l BSD long format
-L NLWP (number of threads) & LWP (thread ID) will be displayed
-ww displays wide format
--forest displays ASCII art process tree
```


### $RANDOM (bash shell variable)
```shell
see also: shuf
echo $RANDOM
echo $(( RANDOM%200+100 ))
```

### route
```shell
Add default route:
route add default gw <gateway addr or name>
```

### rpm/yum
```shell
—nosignature (do not validate GPG sigatures on install)

Show installed files
-qi —filesbytype <package name>

Rebuild rpmdb/broken yum
mv /var/lib/rpm/* /var/tmp/rpm/
rpm —rebuilddb
/usr/lib/rpm/rpmdb_verify /var/lib/rpm/Packages
```

### rsync
```shell
using ssh
rsync --relative --quiet --remove-source-files -e ssh -q /path/to/file.csv deferred@#{worker}:/
```

### sed
```shell
sed s///
app_name=`echo $app | sed -e "s/ /_/g”`
sed -e ‘/s/[[:blank:]]//g’
  
# replace \n
sed -e ':a' -e 'N' -e '$!ba' -e 's/\n/ /g'

# delete from line 2 thru to till word ’status’
cat foo.txt | sed -e ‘2,status/d'

-r Extended Regular Expression argument
echo 198.27.78.5l | sed -r 's/[0-9]{1,3}$/0\/20/'
```

### selinux
```shell
sestatus -v -b
ls -Z <file||dir>
getfacl <file||dir>
setfacl <file|dir>
```

### service (System V init script) (see chkconfig)
```shell
service —status-all
```

### seq
```shell
sequence of numbers
seq <start> <stop>
```

### shuf
```shell
random number generator
see also: od, $RANDOM
shuf -i 1-100 -n 1
```

### socat (port forward)
```shell
nohup socat tcp-l:9999,fork,reuseaddr tcp:appd-po-01p.sys.net:3128  &
```

### sshfs (relies on osxfuse)
```shell
sshfs <host>:<path_to_mount> <local_mount_point>
```

### su/sudo
```shell
sudo -u mradmin /bin/bash

su to no-login user
su -s /bin/ksh csvn

sudoers (/etc/sudoers)
visudoers -f /etc/sudoers
sd ALL = (ALL) ALL
```

### svn
```shell
svn add cf-cli-installer_6.33.1_x86-64.rpm
svn commit -m 'push cf-cli'
```

### systemctl (see also chkconfig)
```shell
disable chronyd.service
enable chronyd.service
status chronyd.service
start chronyd.service
```

### tar
```shell
ssh wilmapp-wc-30s.sys.net "(cd /opt/wily/backup_appd4db-wc-03p/appd/Controller; tar -zcf - .)" |  tar -xzf -
ssh wilmapp-wc-30s.sys.net "(cd /opt/wily/backup_appd4db-wc-03p/appd/Controller/events_service/analytics-processor/bin; tar -zcf - .)" |  tar -xzf -
ssh wilmapp-wc-30s.sys.net "(cd /opt/wily/backup_appd4db-wc-03p/appd/Controller/events_service/analytics-processor/bin; tar -zcf - .)" |  (cd events_service/analytics-processor/bin; tar -xzf -)
```

### tcpdump
```shell
Bit Masking
/usr/sbin/tcpdump -A -s 0 '(((ip[2:2] - ((ip[0]&0xf)<<2)) - ((tcp[12]&0xf0)>>2)) != 0)' | grep 68.87.250.34

host <ip>
src <ip>
dst <ip>
```

### testdisk (data recovery utility)

### toe (table of (terminfo) entries)
```shell
toe -a
```

### vi
```shell
show the difference between tabs and spaces
:set list
:set ff=unix

remove ^M
:1,$ s/<CTRL-V><CTRL-M>//g
```

### wget
```shell
download file 
wget foo.com/index.html -O newfile.html
```

### X
```shell
<configure remote host>
sudo yum install -y xorg-x11-apps xauth libXext libXrender libXtst
sudo vi /etc/ssh/sshd_config
  X11Forwarding yes
  X11UseLocalhost no

sudo /etc/init.d/sshd reload

<from localhost>
xhost + <host>
ssh -X or -Y <host>

<remote host su>
sudo su -
cp /opt/home/white/.Xauthority .
chmod 0600 ~/.Xauthority

# X11 as root:
ssh -XY <user>@remotehost
xeyes
sudo su -
xauth add $(xauth -f /home/<user>/.Xauthority list | tail -1)
xeyes
```
