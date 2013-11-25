LXC Debian Wheezy template
==========================

Notes:

1) You definitely need to change Debian mirror:

MIRROR=${MIRROR:-http://mirror-kt.neolabs.kz/debian}


Changes to original template:

1) In container's /etc/network/interfaces

auto eth0

changed to

allow-hotplug eth0

for faster booting when DHCP server is unavailable (http://lists.debian.org/debian-boot/2007/07/msg00377.html)

2) Set timezone in container as on host

3) Avoid annoying error '/etc/init.d/mountall.sh: 59: kill: Illegal number: 3 1' message during boot (http://lists.debian.org/debian-hurd/2013/08/msg00050.html)

4) Avoid warning via boot: [warn] Mount point '/dev/*' does not exist. Skipping mount. ... (warning).

5) Regenerate ssh keys. By default templates they are rsynced from bootstrap cache (/var/cache/...)

6) Change hostname comment in newly generated keys. By default hostname in regenerated keys are taken from hostname of a host, not container.

7) Create /lib/modules directory. Nessesary if we need to load kernel modules (see lxc.mount.entry later). lxc.cap.drop = sys_module must be unset.

8) Create /dev/ppp device. File permissions are according to default's Wheezy ones.

9) Create /dev/net/tun device. File permissions are according to default's Wheezy ones.

10) Create /dev/fuse device. File permissions are according to default's Wheezy ones.

11) Create /dev/rtc* device and recreate the default's wheezy link.

12) Create convenient uptime utility for container. Now uptime in container shows container's uptime, not the host's one.

13) Added vim, iptables, iputils-ping editor installed in container.

14) Uncommented lxc.cap.drop = sys_module feature to allow container to load modules.

15) Added mounting /lib/modules to container's /lib/modules to allow load kernel modules. Done with AUFS filesystem.
