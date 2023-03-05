# Upload file to container:

## Enable ssh with password

Configure `/etc/ssh/sshd_config`:
```
PermitRootLogin yes
```

## Upload file to container:

Upload file from host to container with ssh:
```
$ scp /path/to/file user@IP:/path/to/file
```