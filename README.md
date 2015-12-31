# shrine-extras

This package contains scripts for installing SHRINE as a service on Red Hat and CentOS Linux systems. These instructions will make your SHRINE installation independent of the account of the user who installed SHRINE, and they will make SHRINE start automatically on boot.

## Instructions

These instructions assume you have already followed the automated install instructions on the SHRINE website and your user account on your SHRINE server has sudo access. `$SHRINE_HOME` is the path to your SHRINE installation, usually `/opt/shrine`. These instructions have been tested with SHRINE version 1.19.1 on Red Hat Enterprise Linux version 6.5.

1. Copy the `common.rc` and `shrine.rc` files that the installer placed in your home directory to `$SHRINE_HOME`.
2. Copy the `runshrine` script to `$SHRINE_HOME`.
2. Create a `shrine` user and `shrine` group on your server. The user account should be a service account with no home directory.
2. Change the owner and group of your SHRINE installation to the shrine user and group: `sudo chown -R shrine:shrine $SHRINE_HOME`.
3. Change the `HOME` variable in the shrine script to your `$SHRINE_HOME`.
4. Copy the `shrine` script to `/etc/init.d`, and make its owner root: `sudo chown root:root /etc/init.d/shrine`.
5. You may now start SHRINE with the following command: `sudo service shrine start`. Similarly, stop SHRINE by invoking `sudo service shrine stop`.
6. To make SHRINE start automatically, run `sudo chkconfig --level 3 shrine on`. This command makes SHRINE start automatically in runlevel 3, which is the default runlevel for Red Hat and CentOS server installations.
7. You likely will want your database management system to start automatically. For example, for MySQL installed using the default packages from CentOS or Red Hat, the command is `sudo chkconfig --level 2345 mysqld on`.
