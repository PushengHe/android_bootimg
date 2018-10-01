# android_bootimg(待验证)
Andorid unpack/repack boot/rececovery.img for windows Thanks @liudongmiao @yyjdelete

1.解包boot.img
bootimg --unpack-bootimg
默认不加文件名的时候，默认是解包boot.img 解包获得文件 kernel 和 ramdisk.gz;
请复制如下解压过程信息，
D:\test>
D:\test>bootimg --unpack-bootimg
arguments: [bootimg file]
bootimg file: boot.img
output: kernel[.gz] ramdisk[.gz] second[.gz]
base: 0x20200000
ramdisk_addr: 0x21200000
second_addr: 0x21100000
tags_addr: 0x20200100
page_size: 2048
name: ""
cmdline: ""
padding_size=2048
arguments: [ramdisk file] [directory]
ramdisk file: ramdisk.gz
directory: initrd
output: cpiolist.txt
compress: True

D:\test>

2.解包 ramdisk.gz (从boot.img 解包获得)
命令： bootimg --unpack-ramdisk 
一般输出 文件名 为 cpiolist.txt 和 目录名为 initrd （注意当前目录不能存在这个目录名的文件夹）

3.打包 ramdisk.gz

命令： bootimg --repack-ramdisk 
注意： 当前目录必须存在 cpiolist.txt 和 inirtd 目录 ,生成新的ramdisk文件，文件名为ramdisk.cpio.gz

4.打包boot.img 

命令： bootimg --repack-bootimg 
特别注意的是 当前目录必须有kernel和ramdisk.cpio.gz ,另外 解包的时候 输出的参数 必须 输入回 打包命令里面

格式应该为 bootimg --repack-bootimg base cmdline page_size padding_size

bootimg --repack-bootimg 0x20200000 2048 2048
