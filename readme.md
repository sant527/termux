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

sudo sshfs -odebug,sshfs_debug,loglevel=debug -o port=8022,ssh_command='ssh -i ~/.ssh/id_rsa_redmi10power_termux',uid=$(id -u simha),gid=$(id -g simha),allow_other,default_permissions u0_a309@192.168.55.104:/data/data/com.termux/files/home /mnt/redmi_termux

the below options

-o port=8022  (if using different port)
uid=$(id -u simha)  (to mount as different user other than root)
gid=$(id -g simha)  (to mount as different group other than root)
ssh_command='ssh -i ~/.ssh/id_rsa_redmi10power_termux.pub'  (to specify a different rsa pub key)
-odebug,sshfs_debug,loglevel=debug  (to show more debugging)

cd /mnt/redmi_termux

sudo umount /mnt/redmi_termux
```

# ssh key gen

```
 $ ssh-keygen       
Generating public/private rsa key pair.
Enter file in which to save the key (/home/simha/.ssh/id_rsa): /home/simha/.ssh/id_rsa_redmi10power_termux       
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/simha/.ssh/id_rsa_redmi10power_termux
Your public key has been saved in /home/simha/.ssh/id_rsa_redmi10power_termux.pub
The key fingerprint is:
SHA256:wG7sNGwl0YaB4ZbzhVvm2sfTOZqzVmXycUDkRcBy8Uk simha@NWLT2218
The key's randomart image is:
+---[RSA 3072]----+
|    .oo+     +=Eo|
|   ..o.oo   ..=o.|
|    = =.=    o.o.|
|   . * X    . + .|
|      @ S    = o |
|     = + . ....  |
|      o . +.+    |
|         .o+ .   |
|         .+o     |
+----[SHA256]-----+

 $ cat ~/.ssh/id_rsa_redmi10power_termux.pub 
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCwh9cw88EYXRiGHzDj0UCiN2yg/uWO40hD4ilMkq547YVVUXjZCKTOoOb4FVfCmYC2b4nsdArMbEavo+1GlQ2dP5FAssEa8tYADlbxDcrKYXNLU/akTN0SnoEyMERhkfltXEbqOrPwZYz7u/xrPkA4ZlpDN/SUMC4ZLNnQNREzCDLTyPQs08Iy4IPzgMDrl0UC/KyaX9Cd7cLCaBIIENX7NBChdnicOjoStCG3mBAkQWJE8UXj5E5I4QaeI21kcUv3B/zbjL9YNANEPtSoHEhcvSbQOxtFve990htKLfqOfxvvWS2NuMSTprjAnOTm5IVujXx5hqkONvY6xgXTuDoo/INEIS9aQSSOk1y1Pkqn5rNYn+pQMupXpQNzXc+aR+8ZZlSJOjodMA/giBPAuH5CwIOVo2ZOE1gEw5TIocShbPKERPqD2VlW5FklH+qiR5faRhqoTV3oy0+dN8hu4YB6DndHG9tbt+40BIQ4i1bmKjaO1IE04V5IFQCqZtdxbWk= simha@NWLT2218

# on termux put the above in this file
~ $ vi ~/.ssh/authorized_keys

```


# install zsh
```
apt install zsh

chsh -s zsh

# create empty file
touch ~/.zshrc

# install wget
apt install wget

# install git
apt install git

# install oh-my-zsh
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

and replace theme as aussiegeek

# change the color .oh-my-zsh/themes/aussiegeek.zsh-theme

PROMPT='$fg_bold[blue][ $fg[yellow]%D{%c} $fg_bold[blue]] $fg_bold[blue] [ $fg[yellow]%n@XXXXXXXXXXX:%~$(git_prompt_info)$fg[yellow]$(ruby_prompt_info)$fg_bold[blue] ]$reset_color
 $ '
# git theming
ZSH_THEME_GIT_PROMPT_PREFIX="$fg_bold[green]("
ZSH_THEME_GIT_PROMPT_SUFFIX=")"
ZSH_THEME_GIT_PROMPT_CLEAN="✔"
ZSH_THEME_GIT_PROMPT_DIRTY="✗"
```

# installing the django server

```
python3 -m venv venv
source venv/bin/activate
pip3 install -r requirements.txt

# start the django server
cd ~/.public_html/django_download/download &&  ~/.public_html/django_download/venv/bin/python3 manage.py runserver 0.0.0.0:8000```
```


# install tmux

```
pkg install tmux

# create a new session
tmux

# attach to the recent session
tmux a

# create windows
ctrl + b, c

# list all windows
ctrl + b, w
```

# check the space

```
# Sort directories w.r.t size
du -ah /storage/emulated/0 --max-depth=1 | sort -hr
```

```
# check the sapce of all mounted
df -h
```


# install mpv
```
for mpv scripts to work use app-api29-universal-debug.apk  app

and add

script=/sdcard/path/to/script.lua
```



# rsync

```
apt install rsync

apt install inotify-tools
```

```
while inotifywait -r -e modify,create,delete,move /storage/emulated/0/tmp; do
   rsync -rtvuc --delete -e 'ssh -p 8022' --progress /storage/emulated/0/tmp/ u0_a52@192.168.0.100:/storage/emulated/0/tmp/
done
```

notice that I added a slash at the end, doing this prevents a new folder from being created

- The parameter -r means recursive, this is, it will copy the contents of the source folder, as well as the contents of every folder inside it.
- The parameter -t makes rsync preserve the modification times of the files that it copies from the source folder.
- The parameter -v means verbose, this parameter will print information about the execution of the command, such as the files that are successfully transferred, so we can use this as a way to keep track of the progress of rsync.



- In order to save bandwidth and time, we can avoid copying the files that we already have in the destination folder that have not been modified in the source folder. To do this, we can add the parameter -u to rsync, this will synchronize the destination folder with the source folder, this is where the delta-transfer algorithm enters. To synchronize two folders like this we use:

```
rsync -rtvu source_folder/ destination_folder/
```
- By default, rsync will take into consideration the date of modification of the file and the size of the file to decide whether the file or part of it needs to be transferred or if the file can be left alone, but we can instead use a hash to decide whether the file is different or not. To do this we need to use the -c parameter, which will perform a checksum in the files to be transferred. This will skip any file where the checksum coincides.

```
rsync -rtvuc source_folder/ destination_folder/
```



# getting filename, downloading and then scp

```
filename=`yt-dlp --get-filename --cookies ~/.public_html/youtube_cookies/youtube.com_cookies.txt --restrict-filenames --no-part --no-mtime -f "${format}" -o "${today}-%(title)s-%(id)s.%(ext)s" "${url}"`

yt-dlp --continue --cookies ~/.public_html/youtube_cookies/youtube.com_cookies.txt --restrict-filenames --no-part --no-mtime --verbose -f "${format}" -o "${today}-%(title)s-%(id)s.%(ext)s" "${url}"


scp -P 8022 /storage/emulated/0/tmp/${filename} u0_a52@192.168.0.100:/storage/emulated/0/tmp/${filename}



and then delete all the files:
```
ssh -p 8022 u0_a52@192.168.0.100<<'ENDSSH'
set -x -o verbose;
rm -rf /storage/emulated/0/tmp/*;
set +x;
ENDSSH
```
```
