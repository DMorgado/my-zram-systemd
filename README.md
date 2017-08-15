# my-zram-systemd

My zram Script for systemd on RHEL 7 / CentOS 7

## Getting Started

This script and unit file will get zram swap working on RHEL7/CentOS7 on default minimal install.

### Prerequisites

Red Hat Enterprise Linux 7, CentOS 7 or similar

Kernel options vm.overcommit_memory, vm.page-cluster, vm.spwapiness have their defaults set in zram script. Check if system defaults are the same. Check variables OVERCOMMIT_MEMORY, PAGE_CLUSTER and SPWAPINESS respectivly

```
vm.overcommit_memory=0
vm.page-cluster=3
vm.spwapiness=60
```

Variable FACTOR in zram script set the % of system RAM used for zram swap, I use 10%, set to whatever you like.

I use as many zram devices as CPUs, because the default kernel doesn't suport compression streams (/sys/block/zram0/max_comp_streams).

### Installing

Copy zram shell script and zram.service unit file to /etc/systemd/system and reload systemd to make it available. Make zram script executable.

```
cp zram zram.service /etc/systemd/system/
chmod +x /etc/systemd/system/zram
systemctl daemon-reload
systemctl enable zram.service
systemctl start zram.service
```

### Tunning Options

After zram is set and started I set this kernel options, change them if you like.

```
vm.overcommit_memory=1
vm.page-cluster=0
vm.spwapiness=100
```
