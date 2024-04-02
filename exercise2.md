you need /home/usr/bin directory 
```cd ~```
```mkdir bin```

create a script called backup_script
```vim backup_script```

in the vim editor, paste this while also changing usr to your username 
```#!/usr/bin/env bash```

```# Directory to be backed up```
```source_dir="/home/your-user/bin"```

```# Backup location```
```backup_dir="/home/your-user/bin-backup"```

```# Rsync command for backup```
```rsync -avzh --delete "$source_dir" "$backup_dir"```

save and exit then change the permissions to execute
```sudo chmod +x backup_script```

in the home directory, create a service file called backup-script.service
```sudo vim backup-script.service```

in the vim editor, paste
```[Unit]```
```Description=Simple Backup Service```

```[Service]```
```Type=oneshot```
```ExecStart=/home/usr/bin/backup_script```

```[Install]```
```WantedBy=multi-user.target```

move this service file to the system directory
```sudo mv ~/backup-script.service /etc/systemd/system/```

make systemd aware of any changes to service files 
```sudo systemctl daemon-reload```

run the service using
```sudo systemctl start backup-script.service```

