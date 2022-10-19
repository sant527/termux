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
ssh -p 8022 u0_a81@192.168.0.101
```

- add id_rsa.pub key to the termux .ssh/authorized_keys

- to get access to storage
> In order to have access to shared storage (/sdcard or /storage/emulated/0), Termux needs a storage access permission. It is not granted by default and is not requested on application startup since it is not necessary for normal application functioning.

- Execute command 

```
termux-setup-storage
```
- run this command on the tv, it will ask to allow for permissions

rsync
```
rsync -rvz -e 'ssh -p 8022' --progress ~/tmp u0_a81@192.168.0.101:/storage/emulated/0/santhosh/vids
```

scp
```
scp -p 8022 /home/administrator/Downloads/termux-app_v0.118.0+github-debug_universal.apk u0_a78@192.168.0.101:/storage/emulated/0/santhosh
```

```
while inotifywait -r -e modify,create,delete,move ~/tmp; do
   rsync -rvz -e 'ssh -p 8022' --progress ~/tmp/ u0_a81@192.168.0.101:/storage/emulated/0/santhosh/vids
done
```

```
tmux new -s rsync

tmux a -t rsync
```

```
while inotifywait -r -e modify,create,delete,move ~/tmp; do
   rsync -avu --delete -e 'ssh -p 8022' --progress ~/tmp/ u0_a81@192.168.0.101:/storage/emulated/0/santhosh/vids
done
```

```
- `-a` Do the sync preserving all filesystem attributes
- `-v` run verbosely
- `-u` only copy files with a newer modification time (or size difference if the times are equal)
- `--delete` delete the files in target folder that do not exist in the source
```
