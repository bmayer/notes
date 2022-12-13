```shell
> stty -F /dev/ttyS0 -a
speed 9600 baud; rows 0; columns 0; line = 0;
intr = ^C; quit = ^\; erase = ^?; kill = ^U; eof = ^D; eol = <undef>; eol2 = <undef>; swtch = <undef>; start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; discard = ^O; min = 1; time = 0;
-parenb -parodd -cmspar cs8 hupcl -cstopb cread clocal -crtscts
-ignbrk -brkint -ignpar -parmrk -inpck -istrip -inlcr -igncr icrnl ixon -ixoff -iuclc -ixany -imaxbel -iutf8
opost -olcuc -ocrnl onlcr -onocr -onlret -ofill -ofdel nl0 cr0 tab0 bs0 vt0 ff0
isig icanon iexten echo echoe echok -echonl -noflsh -xcase -tostop -echoprt echoctl echoke -flusho -extproc
```

```shell=
> dmesg | grep tty
[    0.182449] printk: console [tty0] enabled
[    0.473588] 00:04: ttyS0 at I/O 0x3f8 (irq = 4, base_baud = 115200) is a 16550A
[    0.498048] 0000:08:00.1: ttyS4 at I/O 0xe800 (irq = 31, base_baud = 115200) is a 16550A
[    0.519418] 0000:08:00.2: ttyS5 at I/O 0xe400 (irq = 33, base_baud = 115200) is a 16550A
```

### reading from serial
```shell
cat /dev/ttyS0
cat < /dev/ttyS0
# Exit: Ctrl-A, k, y 

od -x < /dev/ttyS0

socat stdio /dev/ttyS0 

screen /dev/ttyUSB0 9600
```


### RS-232

RS-232 is the standard interface approved by the EIA for connecting serial devices. The standard describes the physical interface and protocol for low-speed communication. The RS-232 protocol is used mostly over DB9 or DB25 ports.
