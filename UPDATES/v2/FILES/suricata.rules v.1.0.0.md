```yaml
alert icmp any any -> any any (msg:"ICMP Echo Request (Ping)"; itype:8; sid:1000001; rev:1;)
alert icmp any any -> any any (msg:"ICMP Echo Reply (Ping Reply)"; itype:0; sid:1000002; rev:1;)
# alert icmp any any -> $HOME_NET any (msg:"ICMP Echo Request (Ping)"; itype:8; sid:1000001; rev:1;)
# alert icmp $HOME_NET any -> any any (msg:"ICMP Echo Reply (Ping Reply)"; itype:0; sid:1000002; rev:1;)
```