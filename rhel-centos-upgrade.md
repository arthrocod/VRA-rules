## CentOS/RHEL upgrade fails due to low space in /boot

With older systems when you keep upgrading kernel, the older one is left behind for rollback reasons. Over the period of time you can end up with several of them. That is fine until /boot mount starts filling up. Also for a better security footprint, it's better to have 2 kernel images and to implement that restriction without fuss just have enough space for 2-3 images in /boot. 
But if the scripts are doing the last 4th or 3rd image cleanup, you may end up in a situation when after an upgrade the system won't come up or worst the upgrade will fail. Then you need to manually remove the older images. 

<pre>
Running transaction check
Transaction check succeeded.
Running transaction test
The downloaded packages were saved in cache until the next successful transaction.
You can remove cached packages by executing 'yum clean packages'.
Error: Transaction test error:
  installing package kernel-core-4.18.0-348.2.1.el8_5.x86_64 needs 26MB on the /boot filesystem
</pre>
Error Summary
-------------
```
Disk Requirements:
   At least 26MB more space needed on the /boot filesystem.

[root@bm-vlan-test01 ~]# ls -l /boot/
total 211808
-rw-r--r--. 1 root root   192173 Aug 10 21:08 config-4.18.0-305.12.1.el8_4.x86_64
-rw-r--r--. 1 root root   192095 Jun  1 11:22 config-4.18.0-305.3.1.el8.x86_64
drwxr-xr-x. 3 root root       17 Sep  2 14:01 efi
drwx------. 4 root root       83 Sep  2 14:05 grub2
-rw-------. 1 root root 86000110 Sep  2 14:04 initramfs-0-rescue-5f707c2c85f74c6dbb2ee924a625c1ed.img
-rw-------. 1 root root 29789144 Sep  2 14:16 initramfs-4.18.0-305.12.1.el8_4.x86_64.img
-rw-------. 1 root root 16246584 Sep  2 14:21 initramfs-4.18.0-305.12.1.el8_4.x86_64kdump.img
-rw-------. 1 root root 29789551 Sep  2 14:16 initramfs-4.18.0-305.3.1.el8.x86_64.img
-rw-------. 1 root root 16246923 Sep  2 14:15 initramfs-4.18.0-305.3.1.el8.x86_64kdump.img
drwxr-xr-x. 3 root root       21 Sep  2 14:03 loader
-rw-------. 1 root root  4165905 Aug 10 21:08 System.map-4.18.0-305.12.1.el8_4.x86_64
-rw-------. 1 root root  4164308 Jun  1 11:22 System.map-4.18.0-305.3.1.el8.x86_64
-rwxr-xr-x. 1 root root 10026120 Sep  2 14:03 vmlinuz-0-rescue-5f707c2c85f74c6dbb2ee924a625c1ed
-rwxr-xr-x. 1 root root 10034312 Aug 10 21:08 vmlinuz-4.18.0-305.12.1.el8_4.x86_64
-rwxr-xr-x. 1 root root 10026120 Jun  1 11:22 vmlinuz-4.18.0-305.3.1.el8.x86_64
[root@bm-vlan-test01 ~]# uname -a 
Linux bm-vlan-test01.qa-pathway-signal-management.cloud 4.18.0-305.12.1.el8_4.x86_64 #1 SMP Wed Aug 11 01:59:55 UTC 2021 x86_64 x86_64 x86_64 GNU/Linux'''
```

There is no need for 4.18.0-305.3.1.el8.x86_64

So to clean/delete the older image tried: 

``` 
yum -q kernenl
yum -y yum-utils
package-cleanup --oldkernels...'''
```
But DNF throws error 
```
[root@bm-vlan-test01 ~]# package-cleanup --oldkernels --count=1
package-cleanup has to be executed with one of the options: --dupes, --leaves, --orphans, --problems or --cleandupes
[root@bm-vlan-test01 ~]# package-cleanup --oldkernels --count=1 --cleandupes
usage: dnf remove [-c [config file]] [-q] [-v] [--version]
                  [--installroot [path]] [--nodocs] [--noplugins]
                  [--enableplugin [plugin]] [--disableplugin [plugin]]
                  [--releasever RELEASEVER] [--setopt SETOPTS] [--skip-broken]
                  [-h] [--allowerasing] [-b | --nobest] [-C] [-R [minutes]]
                  [-d [debug level]] [--debugsolver] [--showduplicates]
                  [-e ERRORLEVEL] [--obsoletes]
                  [--rpmverbosity [debug level name]] [-y] [--assumeno]
                  [--enablerepo [repo]] [--disablerepo [repo] | --repo [repo]]
                  [--enable | --disable] [-x [package]]
                  [--disableexcludes [repo]] [--repofrompath [repo,path]]
                  [--noautoremove] [--nogpgcheck] [--color COLOR] [--refresh]
                  [-4] [-6] [--destdir DESTDIR] [--downloadonly]
                  [--comment COMMENT] [--bugfix] [--enhancement]
                  [--newpackage] [--security] [--advisory ADVISORY]
                  [--bz BUGZILLA] [--cve CVES]
                  [--sec-severity {Critical,Important,Moderate,Low}]
                  [--forcearch ARCH] [--duplicates | --oldinstallonly]
                  [PACKAGE [PACKAGE ...]]
dnf remove: error: unrecognized arguments: --oldkernels --count=1
```
So use dnf instead
```
dnf remove $(dnf repoquery --installonly --latest-limit=-1)
```
