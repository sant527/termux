- install termux not from google play but download apk or fdroid

https://github.com/termux/termux-app/releases

- upgrade and update

```
apt upgrade && apt update

or

pkg upgrade && pkg update
```
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



# install yt-dlp on termux

```
pkg install python
```
```
python3 -m pip install -U yt-dlp
```

# install vim

```
pkg install vim
```


# install iproute2 for ip command
```
apt install iproute2
```

# check ip address
```
ip addr
```

# connect to termux
```
ssh u0_a309@192.168.55.104 -p 8022
```

# install task-spooler

```
apt install task-spooler

eg: ts yt-dlp youtube.com/link
```

# mount redmi using sshfs
```
sudo mkdir /mnt/redmi_termux

sudo sshfs -odebug,sshfs_debug,loglevel=debug -o port=8022,uid=$(id -u simha),gid=$(id -g simha),allow_other,default_permissions u0_a309@192.168.55.104:/data/data/com.termux/files/home /mnt/redmi_termux

-o port=8022  (if using different port)
uid=$(id -u simha)  (to mount as current user

cd /mnt/redmi_termux

sudo unmount /mnt/redmi_termux
```





