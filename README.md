# BBR

## What is it

***BBR*** is Bottleneck Bandwidth and RTT. BBR congestion control computes the sending rate based on the delivery rate (throughput) estimated from ACKs.

BBR was contributed to Linux kernel 4.9 since 2016 by Google.

## How to enable BBR

You need Linux kernel version 4.9 or above

> uname -a
```
Linux 6.1.0-18-amd64
```

## Configure and install

### Available congestion control algo

> sysctl net.ipv4.tcp_available_congestion_control
```
net.ipv4.tcp_available_congestion_control = reno cubic
```

### Active congestion control algo

> sysctl net.ipv4.tcp_congestion_control
```
net.ipv4.tcp_congestion_control = cubic
```

### Activate BBR

> modprobe tcp_bbr
> 
> echo "tcp_bbr" > /etc/modules-load.d/bbr.conf


> sysctl net.ipv4.tcp_available_congestion_control
```
net.ipv4.tcp_available_congestion_control = reno cubic bbr
```


> nano /etc/sysctl.d/bbr.conf
```
net.ipv4.tcp_congestion_control = bbr
net.core.default_qdisc = fq
```


> sysctl -p
> 
> sysctl net.ipv4.tcp_congestion_control
```
net.ipv4.tcp_congestion_control = bbr
```

## Verify that BBR is loaded

> lsmod | grep tcp_bbr
```
tcp_bbr                20480  3
```

## Sources

Information: https://djangocas.dev/blog/huge-improve-network-performance-by-change-tcp-congestion-control-to-bbr

Google open source project BBR: https://github.com/google/bbr

BBR V2 alpha: https://github.com/google/bbr/blob/v2alpha/README.md
