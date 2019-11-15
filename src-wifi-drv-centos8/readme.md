============ rpmfusion packages ============
sudo dnf install --nogpgcheck https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo dnf install --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-8.noarch.rpm 
sudo dnf install --nogpgcheck https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-8.noarch.rpm
sudo dnf config-manager --enable PowerTools
Network controller: Broadcom Inc. and subsidiaries BCM43142 802.11b/g/n (rev 01)

============ install broadcom wifi driver ============
lspci | grep Broadcom
https://www.centos.org/forums/viewtopic.php?f=56&p=302035
yum --skip-broken --nogpgcheck localinstall broadcom-wl-6.30.223.271-13.el7.noarch.rpm akmod-wl-6.30.223.271-30.el7.x86_64.rpm
