Build Wifi Driver

CentOS Version:
cat /etc/centos-release
>> CentOS Linux release 7.6.1810 (Core)

Running Kernel version:
uname -s -r
>> Linux 3.10.0-957.27.2.el7.x86_64

-=-=-=-=-=-=-=-=-=-=-==-=-=-=-=-=-=-=-=-=

1) Install needed tools/packages:

yum grouplist
yum group install 'Development Tools'
yum group update 'Development Tools'

yum install redhat-lsb kernel-abi-whitelists

yum install kernel-devel-$(uname -r)

2) As a regular user (not as root), configure a build tree and minimal .rpmmacros:

mkdir -p ~/rpmbuild/{BUILD,RPMS,SPECS,SOURCES,SRPMS}

echo -e "%_topdir $(echo $HOME)/rpmbuild\n%dist .el$(lsb_release -s -r|cut -d"." -f1).local" >> ~/.rpmmacros

Download wl-kmod*nosrc.rpm

http://elrepo.org/linux/elrepo/el7/SRPMS/wl-kmod-6_30_223_271-5.el7.elrepo.nosrc.rpm

4) Download the Broadcom driver matching your architecture (i.e., 32-bit vs 64-bit):

Linux® STA 64-bit driver:
https://docs.broadcom.com/docs/12358410

from:   http://www.broadcom.com/support/802.11 (external link) (scroll down to "Linux® STA 32-bit (or 64-bit) drivers")

to:      ~/rpmbuild/SOURCES/

5) Build kmod-wl as a regular user (not as root):

### rpmbuild --rebuild --define 'packager <your-name>' /<path-to-nosrc.rpm>/wl-kmod*nosrc.rpm

rpmbuild --rebuild --define 'packager ku' /home/ku/rpmbuild/SOURCES/wl-kmod*nosrc.rpm


6) If ndiswrapper is installed and is no longer needed, then remove it:
yum remove \*ndiswrapper\*


7) Install kmod-wl: (UEFI DISABLED)
rpm -Uvh /home/ku/rpmbuild/RPMS/x86_64/kmod-wl-6_30_223_271-5.el7.local.x86_64.rpm


8) Reboot or to start wireless now:
modprobe wl

9) Store kmod-wl*rpm for safe keeping
###########

10) Optional - Remove the build tree:
rm -rf ~/rpmbuild

