# rpm包的管理
## 用于互联网下载包的打包及安装工具。生成具有.rpm扩展名的文件。RPM是RedHat Package Manager，类似Windows的setup.exe。

## 公认的行业标准。

rpm -qa | grep xx

```
[root@fox01 ~]# rpm -qa | grep firefox
firefox-102.10.0-1.el9.aarch64

[root@fox01 ~]# rpm -q firefox
firefox-102.10.0-1.el9.aarch64

[root@fox01 ~]# rpm -qi firefox
Name        : firefox
Version     : 102.10.0
Release     : 1.el9
Architecture: aarch64
Install Date: 2023年05月31日 星期三 18时36分58秒
Group       : Unspecified
Size        : 273698977
License     : MPLv1.1 or GPLv2+ or LGPLv2+
Signature   : RSA/SHA256, 2023年04月14日 星期五 21时45分58秒, Key ID 05b555b38483c65d
Source RPM  : firefox-102.10.0-1.el9.src.rpm
Build Date  : 2023年04月12日 星期三 17时55分56秒
Build Host  : aarch64-01.stream.rdu2.redhat.com
Packager    : builder@centos.org
Vendor      : CentOS
URL         : https://www.mozilla.org/firefox/
Summary     : Mozilla Firefox Web browser
Description :
Mozilla Firefox is an open-source web browser, designed for standards
compliance, performance and portability.

[root@fox01 ~]# rpm -qf /etc/passwd
setup-2.13.7-9.el9.noarch
```

rpm -e name 卸载rpm包

rpm -ivh rpm包全路径
```
[root@fox01 ~]# rpm -e firefox
[root@fox01 ~]# 
[root@fox01 ~]# rpm -q firefox
未安装软件包 firefox 
[root@fox01 ~]# 
[root@fox01 ~]# rpm -ivh /opt/firefox-102.10.0-1.el9.aarch64.rpm 
警告：/opt/firefox-102.10.0-1.el9.aarch64.rpm: 头V3 RSA/SHA256 Signature, 密钥 ID 8483c65d: NOKEY
Verifying...                          ################################# [100%]
准备中...                          ################################# [100%]
正在升级/安装...
   1:firefox-102.10.0-1.el9           ################################# [100%]
[root@fox01 ~]# 

```












