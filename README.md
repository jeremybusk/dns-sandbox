# dns

This is used for provisioning and deprovisioning stubdns resources

# Files
- dnsmasq.conf
  - Main config. see example ref for syntax
- dnsmasq.hosts
  - This defines name resolutions to override with custom ips.

# Repo Variables
- SSH_KNOWN_HOSTS
  - Contents should be the key lines of the below commands
    - ssh-keyscan -t ed25519 -p 20004 $SSH_HOST
    - ssh-keyscan -t ed25519 -p 20005 $SSH_HOST
- SSH_PUBLIC_KEY
  - Must reside in the /root/.ssh/authorized_keys of each dns stub host
- SSH_SECRET_KEY
  - This is used to connect to the host as root user


# Notes
Getting and adding ssh host public keys
```
ssh-keyscan -t ed25519 -p 20004 $SSH_HOST >> ~/.ssh/known_hosts
```

Disabling strict host checking. Use with caution and never on prod.
```
[[ -f /.dockerenv ]] && echo -e "Host *\n\tStrictHostKeyChecking no\n\n" >> ~/.ssh/config
```

Running local tests
```
ssh root@$SSH_HOST "bash -s" -- < ./localdnstests
```

# More dig
```
dig +trace +recurse +all +qr -t any
```

# Logs
```
tail -f /var/log/syslog
```
