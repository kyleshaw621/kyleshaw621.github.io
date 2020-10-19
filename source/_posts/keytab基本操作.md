---
title: keytab基本操作
date: 2020-10-19 14:16:33
tags: [kerberos, hadoop]
---

# Keytab基本操作

## 显示 keytab 文件列表
```
klist -ket <keytab_file>
```

## 合并 keytab 文件
使用ktutil工具 (进入工具后，输入?可获取帮助)
```
# 命令行输入
ktutil

# 工具内输入
ktutil: rkt <input_keytab1>
ktutil: rkt <input_keytab2>
ktutil: wkt <output_keytab>
```



## 重新生成keytab
进去kadmin.local或者kadmin，然后调用xst即可。
注意，必须加上norandkey参数， 否则生成keytab的时候会更新密码。


```
xst -k /tmp/http.keytab -norandkey HTTP/ubuntu-slave@MyRealm
```
查看密码是否被更新了，也是在kadmin内执行
```
getprinc <princ_name>

```
输出信息如下， 里面就有密码最后的更新时间：
```
Principal: HTTP/ubuntu-master@MyRealm
Expiration date: [never]
Last password change: Thu Jan 09 18:24:21 CST 2020
Password expiration date: [none]
Maximum ticket life: 0 days 10:00:00
Maximum renewable life: 7 days 00:00:00
Last modified: Thu Jan 09 18:24:21 CST 2020 (HTTP/admin@MyRealm)
Last successful authentication: Fri Jan 10 16:29:36 CST 2020
Last failed authentication: Thu Jan 09 20:30:15 CST 2020
Failed password attempts: 0
Number of keys: 4
Key: vno 7, aes256-cts-hmac-sha1-96
Key: vno 7, arcfour-hmac
Key: vno 7, des3-cbc-sha1
Key: vno 7, des-cbc-crc
MKey: vno 1
Attributes: REQUIRES_PRE_AUTH
Policy: [none]
```
