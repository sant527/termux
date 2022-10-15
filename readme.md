- install termux not from google play but download apk or fdroid

- install sshd

```
pkg install openssh
```
- set passwd
```
passwd
```

- know whats the user id
```
id
```

- get ip address

```
ifconfig -a
```
- start sshd server
```
sshd
```

- stop sshd server
```
pkill sshd
```

- check logs
```
logcat -s 'sshd:*'
```

- from another pc access ssh inside termux
```
ssh -p 8022 u0_a78@192.168.0.101
```

