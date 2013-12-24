libvertd
========

# How to run libvertd on port 16509 
By default libertd run as deamon mode, to use with tools like webvert-manager or virt-manager we have to run libvertd service on 16509 port.

  - Install required packages
```
aptitude install xen-utils-common libvirt-bin  qemu-kvm virt-manager

```
  - Configuration 

Edit "/etc/libvirt/libvirtd.conf" and add following options

```
listen_tls = 0
listen_tcp = 1
auth_tcp="none"
tcp_port = "16509"
unix_sock_dir = "/var/run/libvirt"
listen_addr="0.0.0.0"
log_outputs="3:syslog:libvirtd"

```

Edit "/etc/init.d/libvirt-bin" and modify 
```
start-stop-daemon --start --quiet --pidfile $PIDFILE \
                        --exec $DAEMON  -- $libvirtd_opts -l
```

Now once stop and start service libertd
```
/etc/init.d/libvirt-bin stop
/etc/init.d/libvirt-bin start
```



