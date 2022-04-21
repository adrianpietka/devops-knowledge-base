# Iptables

**Accept connection**

```
iptables -I INPUT -p tcp --dport 8080 -j ACCEPT
```

**List rules with line number**

```
iptables -L --line-numbers
```

**Delete rule by line number**

```
iptables -D INPUT 3
```

[List and Delete Iptables Firewall Rule](https://www.digitalocean.com/community/tutorials/how-to-list-and-delete-iptables-firewall-rules)