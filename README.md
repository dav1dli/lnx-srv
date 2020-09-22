# lnx-srv
Linux Server


# Services
## NAMED
dnf install bind bind-utils

Domain: internal
Server: 192.168.100.10
Hostname: master.internal

Forward zone /var/named/internal.db:
```
$TTL 86400
@ IN SOA master.internal. admin.internal. (
                                                2020011800 ;Serial
                                                3600 ;Refresh
                                                1800 ;Retry
                                                604800 ;Expire
                                                86400 ;Minimum TTL
)

;Name Server Information
@ IN NS master.internal.
master IN A 192.168.100.10
internal. IN MX 10 mail.internal.
mail  IN   A 192.168.100.10
dns   IN   A 192.168.100.10
```

Reverse zone /var/named/internal.rev:
```
$TTL 86400
@ IN SOA master.internal. admin.internal. (
                                                2020011800 ;Serial
                                                3600 ;Refresh
                                                1800 ;Retry
                                                604800 ;Expire
                                                86400 ;Minimum TTL
)

@ IN NS master.internal.
master IN A 192.168.100.10

1 IN PTR master.internal.
```

systemctl restart named
firewall-cmd  --add-service=dns --zone=public  --permanent
firewall-cmd --reload
