


### CHS

The CHS values in the actual partition table have pretty restrictive maximum values:

- the cylinders field is just 10 bits wide (= values 0-1023)
- the heads field is 8 bits wide (= values 0-255)
- the sectors field is 6 bits wide (= values 0-63)

```shell
> file armv7.img
armv7.img: DOS/MBR boot sector; 
  partition 1 : ID=0xc, active, start-CHS (0x2,10,9), end-CHS (0xc,60,48), startsector 32768, 163840 sectors; 
  partition 2 : ID=0xa9, start-CHS (0xc,60,49), end-CHS (0x94,141,57), startsector 196608, 2189952 sectors
```

