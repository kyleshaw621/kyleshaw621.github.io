---
title: 解压和生成initrd
date: 2020-10-19 11:41:16
tags:
---

## 解压
如果 initrd 是通过 gzip 压缩的，那可以直接使用以下命令解压
```
zcat <initrd_file> | cpio -div
```

或者手动先解压initrd，然后再用cpio释放文件
```
cpio -div < <uncompress_initrd_file>
```

## 压缩
```
find . | fakeroot cpio -o -H newc | gzip -9 > <new_initrd>
```
